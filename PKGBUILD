# Maintainer: Miles Simpson <miles.a.simpson@gmail.com>

pkgname=stationd-git
pkgver=r143.83b59d8
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
	'1fc36d7061df5571c47c4a4f38e1dadf76240e060f4a57f8da5986d2fc78cff5'
	'eb0ae444e1813cc5b4f3ff5ffebc9fcbba1de79d03cbb5de16e9ef1d2658a7a5')

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
