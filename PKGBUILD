# Maintainer: Miles Simpson <miles.a.simpson@gmail.com>

pkgname=stationd-git
pkgver=r140.bd0c995
pkgrel=1
pkgdesc="UniClOGS stationd housekeeping daemon"
arch=('x86_64' 'aarch64')
url="https://github.com/oresat/uniclogs-software"
license=('GPL3')
depends=('i2c-tools')
makedepends=('git')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=("git+$url.git")
sha256sums=('SKIP')

pkgver() {
	cd "$srcdir/uniclogs-software/${pkgname%-git}"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
	cd "$srcdir/uniclogs-software/${pkgname%-git}"
	./autogen.sh
	mkdir build
	cd build
	../configure --prefix=/usr
	make
}


package() {
	cd "$srcdir/uniclogs-software/${pkgname%-git}/build"
	make DESTDIR="$pkgdir/" install
}
