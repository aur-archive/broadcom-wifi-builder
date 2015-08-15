# Maintainer: William Díaz <wdiaz [at] archlinux [dot] us>
## Maintainer: Alexandr Kotov nektokot at gmail dot com
# broadcom-wl package
# Contributor: Austin ( doorknob60 [at] gmail [dot] com )
# Maintainer: Gaetan Bisson <bisson@archlinux.org>
# broadcom-wifi-builder package
## Maintainer: Paul N. Maxwell <msg [dot] maxwel [at] gmail [dot] com>

pkgname=broadcom-wifi-builder
pkgver=5.100.82.112
_filever=5_100_82_112
pkgrel=2
pkgdesc="Broadcom 802.11abg Networking Drivers Builder"
arch=('i686' 'x86_64')
[ "$CARCH" = "i686" ] && ARCH=x86_32
[ "$CARCH" = "x86_64" ] && ARCH=x86_64
url="http://www.broadcom.com/support/802.11/linux_sta.php"
license=('MIXED/Proprietary')
depends=('linux-headers' 'linux')
install=broadcom-wifi-builder.install
source=( http://www.broadcom.com/docs/linux_sta/hybrid-portsrc_${ARCH}-v${_filever}.tar.gz
        'modprobe.d'
        'linux3.patch'
        'license.patch'
        'semaphore.patch'
        'broadcom-wl'
	'broadcom_abi.patch' )
noextract=(*.tar.gz)
if [ "$CARCH" = "i686" ]; then
_SRC_MD5SUM='62d04d148b99f993ef575a71332593a9'
else
_SRC_MD5SUM='310d7ce233a9a352fbe62c451b2ea309'
fi
md5sums=($_SRC_MD5SUM
         '9e27f32fc90bf7b3045117edb9a58d65'
         '3f79843b6b1a3f7e8041eb8ed86e4ff5'
         '160a6054ceca92db60898852983a42d4'
         '1fc30833a8cc461266e6310fbd15e2f3'
         '740859fc0cfa9473159eaea8611ab876'
         '17884e0b8ae02b12d6c20bd88dd12025')
backup=('etc/modprobe.d/broadcom-wl.conf')

build() {
  install -d -m 755 ${pkgdir}/usr/src/broadcom-wl
  cd ${pkgdir}/usr/src/broadcom-wl
  tar -xvf ${srcdir}/hybrid-portsrc_${ARCH}-v${_filever}.tar.gz

  patch -p1 -i "${srcdir}/linux3.patch"
  patch -p1 -i "${srcdir}/license.patch"
  patch -p1 -i "${srcdir}/semaphore.patch"
  patch -p1 -i "${srcdir}/broadcom_abi.patch"

  install -D -m 755 ${srcdir}/broadcom-wl ${pkgdir}/etc/rc.d/broadcom-wl
  install -d -m 755 ${pkgdir}/usr/share/licenses/${pkgname}
  ln -s /usr/src/broadcom-wl/lib/LICENSE.txt "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -D -m 644 ${srcdir}/modprobe.d "${pkgdir}"/etc/modprobe.d/broadcom-wl.conf
}

