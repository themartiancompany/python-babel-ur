# Maintainer: Morten Linderud <foxboron@archlinux.no>
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor : Giedrius Slavinskas <giedrius25@gmail.com>

pkgname=python-babel
pkgver=2.14.0
_core=42
pkgrel=1
pkgdesc="A collection of tools for internationalizing Python applications"
url="http://babel.pocoo.org/"
license=("BSD")
arch=('any')
depends=('python' 'python-pytz')
makedepends=('python-setuptools')
checkdepends=('python-pytest' 'python-freezegun')
noextract=("cldr-core-$_core.zip")
source=("$pkgname-$pkgver.tar.gz::https://github.com/python-babel/babel/archive/v$pkgver.tar.gz"
        "cldr-core-$_core.zip::http://unicode.org/Public/cldr/$_core/core.zip"
        "cldr-common-$_core.0.zip::http://unicode.org/Public/cldr/$_core/cldr-common-$_core.0.zip")
sha256sums=('ad76eab6905b626d7d4110d2032bc60c69bef225ec94c67d7229425ebe53f659'
            '53cd4fd1ac2ee4d4cbcae362e7af5d02e98e5e39c826ce9d723d41ca836fc846'
            '53cd4fd1ac2ee4d4cbcae362e7af5d02e98e5e39c826ce9d723d41ca836fc846')

prepare() {
  cp "$srcdir"/cldr-core-$_core.zip babel-$pkgver/cldr/cldr-core-$_core.zip
  cp "$srcdir"/cldr-common-$_core.0.zip babel-$pkgver/cldr/cldr-common-$_core.0.zip
}

build(){
  cd "babel-$pkgver"
  python setup.py import_cldr
  python setup.py build
}

check(){
  cd "babel-$pkgver"
  # the tests fail if running in the wrong timezone:
  # https://github.com/python-babel/babel/issues/757
  TZ=UTC pytest -k 'not test_setuptools_commands'
}

package_python-babel() {
  cd "babel-$pkgver"
  python setup.py install --root="$pkgdir" --optimize=1 --skip-build
  install -D -m0644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
