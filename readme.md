# Legion Go Kernel on Arch
Simple Legion GO `PKGBUILD` kernel file based on the `linux-lts` `PKGBUILD`
with patches that fix the white flashing issue
and frame halving on 60hz, as well as add in fsync.
With these patches, the Legion Go is perfectly usable on Linux.

The patches were taken from https://copr.fedorainfracloud.org/coprs/sentry/kernel-fsync/ , so if you are on a Fedora based distro, you
can use that kernel instead.

Instructions:
```bash
makepkg -s
sudo pacman -U linux-legiongo-6.6.14-1-x86_64.pkg.tar.zst
sudo pacman -U linux-legiongo-headers-6.6.14-1-x86_64.pkg.tar.zst
```

The current version builds from kernel 6.6.14, since that was
the kernel used in fsync at the time of this writing.