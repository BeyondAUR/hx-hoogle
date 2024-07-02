# Maintainer: Evan Greenup <evan_greenup@protonmail.com>
_name=hoogle
pkgname=hx-${_name}
pkgver=5.0.18.4
pkgrel=1
license=("BSD-3-Clause")
arch=('x86_64')
url="https://github.com/ndmitchell/hoogle"
depends=(zlib )
makedepends=(stack cabal-install)
provides=("hoogle")
conflicts=("hoogle")
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/ndmitchell/hoogle/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('f42e1da527d3217e1adbb82c9611b945341b76b1fc85f47f9c04d711c73baf95')

_resolver=nightly

prepare() {
  cabal v2-update
}

build() {
  cd "${srcdir}/${_name}-${pkgver}"

  cabal v2-build --with-compiler=$(stack --resolver=${_resolver} path --compiler-exe)
}

check() {
  cd "${srcdir}/${_name}-${pkgver}"
  cabal v2-test --with-compiler=$(stack --resolver=${_resolver} path --compiler-exe) --enable-tests
}

package() {
  cd "${srcdir}/${_name}-${pkgver}"
  mkdir -m755 -p "${pkgdir}/usr/bin/"
  install -m755 "$(cabal list-bin --with-compiler=$(stack --resolver=${_resolver} path --compiler-exe) hoogle)" "${pkgdir}/usr/bin/hoogle"
  chmod 755 "${pkgdir}/usr/bin/hoogle"
  mkdir -m755 -p "${pkgdir}/usr/share/licenses/${pkgname}"
  install -D -m644 "LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
