# Maintainer: Martin Braun
# Contributor: Noa Himesaka
# Contributor: Redecorating
# Contributors: There are many more, see `grep -h "From:" *.patch|sort|uniq -c`
#               at https://github.com/NoaHimesaka1873/linux-t2-arch.
#               Additionally, MrARM and Ronald Tschalär wrote apple-bce and
#               apple-ibridge drivers, respectively.

pkgbase=linux-t2-bin
pkgname=(
    linux-t2-bin
    linux-t2-headers-bin
)
pkgver=7.2.9.arch1
_upstream_pkgrel=1
pkgrel="${_upstream_pkgrel}.1"

pkgdesc='Prebuilt Linux for T2 Macs'
arch=('x86_64')
url='https://github.com/NoaHimesaka1873/linux-t2-arch'
license=('GPL-2.0-only')
options=('!debug' '!strip')

makedepends=('libarchive')

_kernel="linux-t2-${pkgver}-${_upstream_pkgrel}-${CARCH}.pkg.tar.zst"
_headers="linux-t2-headers-${pkgver}-${_upstream_pkgrel}-${CARCH}.pkg.tar.zst"

source=(
    "https://github.com/NoaHimesaka1873/linux-t2-arch/releases/download/v${pkgver}/${_kernel}"
    "https://github.com/NoaHimesaka1873/linux-t2-arch/releases/download/v${pkgver}/${_headers}"
)

noextract=(
    "${_kernel}"
    "${_headers}"
)

sha256sums=('87206ce8640c96cc561ca654a6c2521ea6cc15a4e26ae2c8d8e1cc85d38641c0'
            'd96e12f966d05115ce65dc30d5a1da681b5deb4db29956aeb6007ea873bd73ce')

package_linux-t2-bin() {
    pkgdesc='Prebuilt Linux kernel and modules for T2 Macs'
    depends=(
        coreutils
        initramfs
        kmod
    )
    optdepends=(
        "linux-t2-headers-bin: prebuilt headers and scripts for building modules"
        'linux-firmware: firmware images needed for some devices'
        'scx-scheds: to use sched-ext schedulers'
        'wireless-regdb: to set the correct wireless channels of your country'
    )
    provides=(
        "linux-t2=${pkgver}-${_upstream_pkgrel}"
        "linux=${pkgver}"
        KSMBD-MODULE
        NTSYNC-MODULE
        VIRTUALBOX-GUEST-MODULES
        WIREGUARD-MODULE
    )
    conflicts=(
        linux-t2
        apple-gmux-t2-dkms-git
    )
    replaces=(
        apple-gmux-t2-dkms-git
        virtualbox-guest-modules-arch
        wireguard-arch
    )
    bsdtar -xpf "$srcdir/$_kernel" -C "$pkgdir" \
        --exclude='.PKGINFO' \
        --exclude='.BUILDINFO' \
        --exclude='.MTREE' \
        --exclude='.INSTALL' \
        --exclude='.CHANGELOG'
}

package_linux-t2-headers-bin() {
    pkgdesc='Prebuilt headers and scripts for building modules for the T2 Mac kernel'
    depends=(
        binutils
        glibc
        libelf
        libgcc
        openssl
        pahole
        xxhash
        zlib
        zstd
    )
    provides=(
        "linux-t2-headers=${pkgver}-${_upstream_pkgrel}"
        LINUX-HEADERS
        linux-headers
    )
    conflicts=(
        linux-t2-headers
    )
    bsdtar -xpf "$srcdir/$_headers" -C "$pkgdir" \
        --exclude='.PKGINFO' \
        --exclude='.BUILDINFO' \
        --exclude='.MTREE' \
        --exclude='.INSTALL' \
        --exclude='.CHANGELOG'
}
