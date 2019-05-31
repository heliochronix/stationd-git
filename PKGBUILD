# Maintainer: Miles Simpson <miles.a.simpson@gmail.com>

pkgname=stationd-git
pkgver=r141.c4bbb0c
pkgrel=1
pkgdesc="UniClOGS stationd housekeeping daemon"
arch=('x86_64' 'aarch64')
url="https://github.com/oresat/uniclogs-software"
license=('GPL3')
depends=('i2c-tools')
makedepends=('git')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=("git+$url.git"
	'stationd.conf'
	'stationd.service')
sha256sums=('SKIP'
	'8d08e03615a5cfd7e798ffc5916cfd712c26a0aed0211eda32d3c4e62eddd24d'
	'9cdff0af127740ad53f1ecca5d798c2ffed64a418553babb8e89b75d3ec76ce8')

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
	install -Dm0644 "${srcdir}"/stationd.service "${pkgdir}"/usr/lib/systemd/system/stationd.service
	install -Dm0644 "${srcdir}"/stationd.conf "${pkgdir}"/usr/lib/tmpfiles.d/stationd.conf
}
