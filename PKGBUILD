# Contributor: dale <dale@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>

pkgname=rockdodger
pkgver=0.6
pkgrel=2
pkgdesc="Space Rocks is a game - Dodge the space rocks, use your shields, fire your thrusters, cross your fingers, and kiss your ship goodbye"
arch=('i686' 'x86_64')
url="http://spacerocks.sourceforge.net/"
license=('GPL')
depends=('sdl' 'sdl_mixer' 'sdl_image')
install=rockdodger.install
source=(http://downloads.sourceforge.net/spacerocks/${pkgname}-${pkgver}.tar.gz rockdodger-0.6.0a-gcc41.patch)
md5sums=('a82a564a6530e60e7f041f7d95c4cae8' 'c8b17a6ffaa12f1a116170437b4629c0')

build() {
 cd ${srcdir}/${pkgname}-${pkgver}
 patch -Np0 -i ../rockdodger-0.6.0a-gcc41.patch || return 1
 sed -i 's|/usr/share/rockdodger/.highscore|/var/games/rockdodger.highscore|' main.c || return 1
 sed -i "s|\./data|/usr/share/rockdodger/data|" main.c || return 1
 sed -i -e "s:-g:${CFLAGS}:" Makefile || return 1
 make || return 1

 install -D -m755 rockdodger ${pkgdir}/usr/bin/rockdodger
 install -d ${pkgdir}/usr/share/rockdodger/data
 install -m644 data/*.{bmp,png,wav,mod} ${pkgdir}/usr/share/rockdodger/data

 chown root:games ${pkgdir}/usr/bin/rockdodger
 chmod 2755 ${pkgdir}/usr/bin/rockdodger
 install -d ${pkgdir}/var/games
 chown root:games ${pkgdir}/var/games
 chmod 775 ${pkgdir}/var/games
}
