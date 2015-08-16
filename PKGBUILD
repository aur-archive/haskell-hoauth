# Maintainer: Arch Haskell Team <arch-haskell@haskell.org>
_hkgname=hoauth
pkgname=haskell-hoauth
pkgver=0.3.2.1
pkgrel=3
pkgdesc="A Haskell implementation of OAuth 1.0a protocol."
url="http://hackage.haskell.org/package/${_hkgname}"
license=('custom:BSD3')
arch=('i686' 'x86_64')
makedepends=()
depends=('ghc' 'haskell-rsa>=1.0.5' 'haskell-sha>=1.4.1.1' 'haskell-binary>=0.5.0.2' 'haskell-bytestring=0.9.1.7' 'haskell-curl>=1.3.5' 'haskell-dataenc>=0.13.0.2' 'haskell-mtl>=1.1.0.2' 'haskell-old-locale=1.0.0.2' 'haskell-random=1.0.0.2' 'haskell-time=1.1.4' 'haskell-utf8-string>=0.3.4')
options=('strip')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/${pkgver}/${_hkgname}-${pkgver}.tar.gz)
install=${pkgname}.install
build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure -O --enable-split-objs --enable-shared \
       --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}
package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
    install -D -m644 LICENSE ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
    rm -f ${pkgdir}/usr/share/doc/${pkgname}/LICENSE
}
md5sums=('39a9cc09bebe73f8452d7b6834b6b9e7')
