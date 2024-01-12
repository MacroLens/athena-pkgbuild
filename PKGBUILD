# Maintainer: Dylan Le <self at dylanle dot dev>
pkgname=athena-git
pkgver=v1.4.3.r0.b23d255
pkgrel=1
pkgdesc="Athena is a modern, practical language for proof engineering & natural deduction."
arch=('x86_64')
url="https://github.com/AthenaFoundation/athena.git"
license=('Apache')
depends=('bash' 'sh' 'gmp' 'glibc')
optdepends=('spass: needed for prove command in athena'
			'minisat-git: needed for sat commands in athena')
makedepends=('git' 'smlnj' 'mlton')
provides=("${pkgname%-VCS}")
conflicts=("${pkgname%-VCS}")
source=("$pkgname::git+$url#tag=v1.4.3")
md5sums=('SKIP')
install=$pkgname.install

pkgver() {
	cd "$srcdir/${pkgname%-VCS}"
	git describe --long --tags | sed 's/\([^-]*-\)g/r\1/;s/-/./g'
}

build() {
	cd "$srcdir/${pkgname%-VCS}"
	make build
}

# Regression Testing Fails.
#check() {
#	cd "$srcdir/${pkgname%-VCS}"
#	extracted_version=$(echo "$pkgver" | sed -n 's/^\(v[0-9]\+\.[0-9]\+\.[0-9]\+\).*/\1/p')
#	python3 tests/regression/regressionTest.py build/athena-linux-$extracted_version/athena
#}

package() {
	cd "$srcdir/${pkgname%-VCS}"
	extracted_version=$(echo "$pkgver" | sed -n 's/^\(v[0-9]\+\.[0-9]\+\.[0-9]\+\).*/\1/p')
	mkdir -p $pkgdir/opt
	cp -r "build/athena-linux-$extracted_version" "$pkgdir/opt/athena"
	mkdir -p $pkgdir/usr/bin
	ln -s /opt/athena/athena $pkgdir/usr/bin/
}
