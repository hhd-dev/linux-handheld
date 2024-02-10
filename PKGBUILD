pkgbase=linux-legiongo
pkgver=6.6.14
pkgrel=1
pkgdesc='LTS Linux'
url='https://www.kernel.org'
arch=(x86_64)
license=(GPL2)
makedepends=(
  bc
  cpio
  gettext
  libelf
  pahole
  perl
  python
  tar
  xz

  # htmldocs
  graphviz
  imagemagick
  python-sphinx
  texlive-latexextra
)
options=('!strip')
_srcname=linux-$pkgver
_srctag=v$pkgver
source=(
  https://cdn.kernel.org/pub/linux/kernel/v${pkgver%%.*}.x/${_srcname}.tar.{xz,sign}
  # 0001-ZEN-Add-sysctl-and-CONFIG-to-disallow-unprivileged-C.patch
  # 0002-skip-simpledrm-if-nvidia-drm.modeset=1-is.patch
  # 0003-Default-to-maximum-amount-of-ASLR-bits.patch
  # 0005-fix-doc-build.patch

  # linux-fsync patches
  tkg.patch
  fsync.patch
  # OpenRGB.patch
  amdgpu-si-cik-default.patch
  # winesync.patch
  tkg-BBRv2.patch
  tkg-bcachefs.patch
  tkg-misc-additions.patch
  tkg-unprivileged-CLONE_NEWUSER.patch

  # device specific patches
  # linux-surface.patch
  steam-deck.patch
  steam-deck-valve15.patch
  # asus-linux.patch
  # lenovo-legion-laptop.patch
  #  workaround for i915 getting stuck during async page flips on Nvidia PRIME systems
  0001-drm-i915-quirks-disable-async-flipping-on-specific-d.patch
  0002-drm-i915-add-kernel-parameter-to-disable-async-page-.patch
  # ROG Ally
  # rog-ally-audio-fix.patch
  # ROG-ALLY-NCT6775-PLATFORM.patch
  # v10-0001-HID-asus-fix-more-n-key-report-descriptors-if-n-.patch
  # v10-0002-HID-asus-make-asus_kbd_init-generic-remove-rog_n.patch
  # v10-0003-HID-asus-add-ROG-Ally-N-Key-ID-and-keycodes.patch
  # v10-0004-HID-asus-add-ROG-Ally-xpad-settings.patch
  # rog-ally-bmc150.patch

  # hdr: https://github.com/CachyOS/kernel-patches
  0001-amd-hdr.patch
  0001-add-acpi_call.patch
  uinput.patch

  # steamdeck oled patches
  steamdeck-oled-wifi.patch
  steamdeck-oled-bt.patch
  steamdeck-oled-audio.patch
  steamdeck-oled-hw-quirks.patch

  # temporary patches
  0001-Remove-REBAR-size-quirk-for-Sapphire-RX-5600-XT-Puls.patch
  mt76:-mt7921:-Disable-powersave-features-by-default.patch
  0001-acpi-proc-idle-skip-dummy-wait.patch
  # Fixes the steam deck not coming back from hibernation
  0001-Revert-nvme-pci-drop-redundant-pci_enable_pcie_error.patch
  # Allows corectl to work out of the box
  0001-Set-amdgpu.ppfeaturemask-0xffffffff-as-default.patch

  # Allow to set custom USB pollrate for specific devices like so:
  # usbcore.interrupt_interval_override=045e:00db:16,1bcf:0005:1
  # useful for setting polling rate of wired PS4/PS5 controller to 1000Hz
  # https://github.com/KarsMulder/Linux-Pollrate-Patch
  # https://gitlab.com/GloriousEggroll/nobara-images/-/issues/64
  # 0001-Allow-to-set-custom-USB-pollrate-for-specific-device.patch

  # # Also set the PS controller bluetooth polling rate to 1000Hz
  # set-ps4-bt-poll-rate-1000hz.patch
)
validpgpkeys=(
  ABAF11C65A2970B130ABE3C479BE3E4300411886  # Linus Torvalds
  647F28654894E3BD457199BE38DBBDC86092693E  # Greg Kroah-Hartman
)
# https://www.kernel.org/pub/linux/kernel/v6.x/sha256sums.asc
sha256sums=('fbe96b2db3f962cd2a96a849d554300e7a4555995160082d4f323c2a1dfa1584'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP')

export KBUILD_BUILD_HOST=archlinux
export KBUILD_BUILD_USER=$pkgbase
export KBUILD_BUILD_TIMESTAMP="$(date -Ru${SOURCE_DATE_EPOCH:+d @$SOURCE_DATE_EPOCH})"

prepare() {
  cd $_srcname

  echo "Setting version..."
  echo "-$pkgrel" > localversion.10-pkgrel
  echo "${pkgbase#linux}" > localversion.20-pkgname

  local src
  for src in "${source[@]}"; do
    src="${src%%::*}"
    src="${src##*/}"
    src="${src%.zst}"
    [[ $src = *.patch ]] || continue
    echo "----- Applying patch $src..."
    patch -Np1 < "../$src"
  done

  echo "Setting config..."
  cp ../config .config
  make olddefconfig
  diff -u ../config .config || :

  make -s kernelrelease > version
  echo "Prepared $pkgbase version $(<version)"
}

build() {
  cd $_srcname
  make all
  make htmldocs
}

_package() {
  pkgdesc="The $pkgdesc kernel and modules"
  depends=(
    coreutils
    initramfs
    kmod
  )
  optdepends=(
    'wireless-regdb: to set the correct wireless channels of your country'
    'linux-firmware: firmware images needed for some devices'
  )
  provides=(
    KSMBD-MODULE
    VIRTUALBOX-GUEST-MODULES
    WIREGUARD-MODULE
  )
  replaces=(
    wireguard-lts
  )

  cd $_srcname
  local modulesdir="$pkgdir/usr/lib/modules/$(<version)"

  echo "Installing boot image..."
  # systemd expects to find the kernel here to allow hibernation
  # https://github.com/systemd/systemd/commit/edda44605f06a41fb86b7ab8128dcf99161d2344
  install -Dm644 "$(make -s image_name)" "$modulesdir/vmlinuz"

  # Used by mkinitcpio to name the kernel
  echo "$pkgbase" | install -Dm644 /dev/stdin "$modulesdir/pkgbase"

  echo "Installing modules..."
  ZSTD_CLEVEL=19 make INSTALL_MOD_PATH="$pkgdir/usr" INSTALL_MOD_STRIP=1 \
    DEPMOD=/doesnt/exist modules_install  # Suppress depmod

  # remove build link
  rm "$modulesdir"/build
}

_package-headers() {
  pkgdesc="Headers and scripts for building modules for the $pkgdesc kernel"
  depends=(pahole)

  cd $_srcname
  local builddir="$pkgdir/usr/lib/modules/$(<version)/build"

  echo "Installing build files..."
  install -Dt "$builddir" -m644 .config Makefile Module.symvers System.map \
    localversion.* version vmlinux
  install -Dt "$builddir/kernel" -m644 kernel/Makefile
  install -Dt "$builddir/arch/x86" -m644 arch/x86/Makefile
  cp -t "$builddir" -a scripts

  # required when STACK_VALIDATION is enabled
  install -Dt "$builddir/tools/objtool" tools/objtool/objtool

  # required when DEBUG_INFO_BTF_MODULES is enabled
  install -Dt "$builddir/tools/bpf/resolve_btfids" tools/bpf/resolve_btfids/resolve_btfids

  echo "Installing headers..."
  cp -t "$builddir" -a include
  cp -t "$builddir/arch/x86" -a arch/x86/include
  install -Dt "$builddir/arch/x86/kernel" -m644 arch/x86/kernel/asm-offsets.s

  install -Dt "$builddir/drivers/md" -m644 drivers/md/*.h
  install -Dt "$builddir/net/mac80211" -m644 net/mac80211/*.h

  # https://bugs.archlinux.org/task/13146
  install -Dt "$builddir/drivers/media/i2c" -m644 drivers/media/i2c/msp3400-driver.h

  # https://bugs.archlinux.org/task/20402
  install -Dt "$builddir/drivers/media/usb/dvb-usb" -m644 drivers/media/usb/dvb-usb/*.h
  install -Dt "$builddir/drivers/media/dvb-frontends" -m644 drivers/media/dvb-frontends/*.h
  install -Dt "$builddir/drivers/media/tuners" -m644 drivers/media/tuners/*.h

  # https://bugs.archlinux.org/task/71392
  install -Dt "$builddir/drivers/iio/common/hid-sensors" -m644 drivers/iio/common/hid-sensors/*.h

  echo "Installing KConfig files..."
  find . -name 'Kconfig*' -exec install -Dm644 {} "$builddir/{}" \;

  echo "Removing unneeded architectures..."
  local arch
  for arch in "$builddir"/arch/*/; do
    [[ $arch = */x86/ ]] && continue
    echo "Removing $(basename "$arch")"
    rm -r "$arch"
  done

  echo "Removing documentation..."
  rm -r "$builddir/Documentation"

  echo "Removing broken symlinks..."
  find -L "$builddir" -type l -printf 'Removing %P\n' -delete

  echo "Removing loose objects..."
  find "$builddir" -type f -name '*.o' -printf 'Removing %P\n' -delete

  echo "Stripping build tools..."
  local file
  while read -rd '' file; do
    case "$(file -Sib "$file")" in
      application/x-sharedlib\;*)      # Libraries (.so)
        strip -v $STRIP_SHARED "$file" ;;
      application/x-archive\;*)        # Libraries (.a)
        strip -v $STRIP_STATIC "$file" ;;
      application/x-executable\;*)     # Binaries
        strip -v $STRIP_BINARIES "$file" ;;
      application/x-pie-executable\;*) # Relocatable binaries
        strip -v $STRIP_SHARED "$file" ;;
    esac
  done < <(find "$builddir" -type f -perm -u+x ! -name vmlinux -print0)

  echo "Stripping vmlinux..."
  strip -v $STRIP_STATIC "$builddir/vmlinux"

  echo "Adding symlink..."
  mkdir -p "$pkgdir/usr/src"
  ln -sr "$builddir" "$pkgdir/usr/src/$pkgbase"
}

# _package-docs() {
#   pkgdesc="Documentation for the $pkgdesc kernel"

#   cd $_srcname
#   local builddir="$pkgdir/usr/lib/modules/$(<version)/build"

#   echo "Installing documentation..."
#   local src dst
#   while read -rd '' src; do
#     dst="${src#Documentation/}"
#     dst="$builddir/Documentation/${dst#output/}"
#     install -Dm644 "$src" "$dst"
#   done < <(find Documentation -name '.*' -prune -o ! -type d -print0)

#   echo "Adding symlink..."
#   mkdir -p "$pkgdir/usr/share/doc"
#   ln -sr "$builddir/Documentation" "$pkgdir/usr/share/doc/$pkgbase"
# }

pkgname=(
  "$pkgbase"
  "$pkgbase-headers"
  "$pkgbase-docs"
)
for _p in "${pkgname[@]}"; do
  eval "package_$_p() {
    $(declare -f "_package${_p#$pkgbase}")
    _package${_p#$pkgbase}
  }"
done

# vim:set ts=8 sts=2 sw=2 et:
