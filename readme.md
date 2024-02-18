# Linux-Handheld for Arch
A collection of patches for various devices made for Arch.
Adds fixes for the Ally, Legion Go, and bmi160, bmi260, bmi323 devices.
Based on 6.6 linux-lts, with the patches from the Fedora 
[kernel-fsync](https://copr.fedorainfracloud.org/coprs/sentry/kernel-fsync/) kernel
and some additional ones (such as the bmi160 fix for Ayaneo devices and others).

It includes the winesync patch series and the preferred core patch series from
upstream, so it is a viable candidate instead of a newer 6.7+ kernel which
might introduce additional regressions.

For the Legion Go, fixes the white flashing issue
and frame halving on 60hz, as well as add in fsync.
It also backports the upcoming xpad and rotation patches, so you do not need
to use the kernel param/udev xpad rule to use the legion go.
With these patches, the Legion Go is up to par with Windows on Linux.
Except for auto-vram still exhibiting issues.

For the Ally, fixes the speakers, controller wake from sleep, includes the latest
controller patch series, and the IMu patch series.

A majority of the patches were taken from https://copr.fedorainfracloud.org/coprs/sentry/kernel-fsync/, 
so if you are on a Fedora based distro, you can use that kernel instead.
However, it misses the additional IMU patches required for certain
handhelds to work, which are added on top.

Instructions:
```bash
git clone https://github.com/hhd-dev/linux-handheld
cd linux-handheld/6.6

makepkg -s
sudo pacman -U linux-handheld-*
```