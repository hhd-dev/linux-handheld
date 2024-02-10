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

  # legion go upstream patches
  legion-go-display-quirk.patch
  legion-go-controllers.patch

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
  config
)
validpgpkeys=(
  ABAF11C65A2970B130ABE3C479BE3E4300411886  # Linus Torvalds
  647F28654894E3BD457199BE38DBBDC86092693E  # Greg Kroah-Hartman
)
# https://www.kernel.org/pub/linux/kernel/v6.x/sha256sums.asc
sha256sums=('fbe96b2db3f962cd2a96a849d554300e7a4555995160082d4f323c2a1dfa1584'
            'SKIP'
            'a33a2b55fe3ea04ce86c4ccade0afac9825159a95bdc9cfbd1a464030dba3b33'
            '9df628fd530950e37d31da854cb314d536f33c83935adf5c47e71266a55f7004'
            '65dcacafd156b33290f8b43a661b5ab09ed7583e4a1f2c6331b9155497233f60'
            '1e368d0290978329562e19cba044794dd0d5e8e8a40a43086ff7fe1aa56afaf4'
            '7db5b4e6383323a8428835a13db38611e78799c93b35b6858ab30bab8855f745'
            '4183cd4cb1031d269eb3f459cdbfc3cd1c4726b5df08c493c41ee1610601f27c'
            '3bc71559122c9c37dc7ca1f08148dd48978dd8d0ccdb1454c20a4308f0aa2e13'
            'ab145b33869e83ef07012ead518a7eef52ac6c39a740712b0a37bf2dd15cef5a'
            '878dd43202bde383e2ada287b836b3026ce65cd014d0f0fadb787c5db4bf6d99'
            '5c3ac67f610eb26fb89fdf9704338728603b63771c17143568f7d13bf3f7bade'
            '65f9f99ca97dff0df9232dc1325f01575e2d97f34a33f4e6db3874e80cd3fcb6'
            '02347bc7d215f1cac1ba7b65eef9f88fc38c6dec535b425b45bfaa2f6e19e211'
            'ce73a89c7ce523d0009f1f384524587113db3d30f759d751203e68fef237b620'
            '5a3df4533db108a720386236b61f1b73ce157d3f303edc3d0f9e560cd7fd2768'
            '5a2aa1c97adef776c4c900f74a2bb096738f7736e590adf73803f3766edec74b'
            '5c382998db205310f2372b1c65a56012564b8125fbd4dfe7b108ef7441643f6e'
            '34864acac427928c641a90ffeef74da74a89cf00f6fba4560343e1813805d75e'
            'ead752b5088b04b38d1fcdb98cb6e6d6545ee736e71a56b3dd4466198e7b8325'
            '6680266ef50333fae7a10684ac8de9dc6c255b1288d5717501d5819a28b7cb9b'
            'e5e1a267dae61fa2a82d17b4f063a3c7bacbedf108d55ede3526f1121d299421'
            '064bd6de567bd5ec7b9b6c5562fb360e247373971a77cd98ff97c4e3356589a8'
            '4c574391fac5f00b10981022321608f2bb655ea15a6ff0ffdcb4f096161683f6'
            'd8bf9fa316fb6a5057f38ebf2ed55c9678b9c1fde52c0b46f72b8e8d8721ec6f'
            'f528e75c615c571a42861eb56c15ede9f6b81c2e64fe017a518282ea18e54c21'
            '38db1ffbacc2315df6ec862404e0dfe73360f950c75336a960b9da382b2a8e7d'
            '6d02772dfbc7805812be3082f0c0052fbbc0f317d71cc3f34692440641a2b9f0')

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
  # make htmldocs
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

  # echo "Removing documentation..."
  # rm -r "$builddir/Documentation"

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
  # "$pkgbase-docs"
)
for _p in "${pkgname[@]}"; do
  eval "package_$_p() {
    $(declare -f "_package${_p#$pkgbase}")
    _package${_p#$pkgbase}
  }"
done

# vim:set ts=8 sts=2 sw=2 et:
