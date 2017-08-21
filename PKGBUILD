# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor : Giedrius Slavinskas <giedrius25@gmail.com>

pkgbase=python-babel
pkgname=(python-babel python2-babel)
pkgver=2.5.0
pkgrel=1
pkgdesc="A collection of tools for internationalizing Python applications"
url="http://babel.pocoo.org/"
license=("BSD")
arch=('any')
makedepends=('python' 'python2'
	    'python-setuptools' 'python2-setuptools'
	    'python-pytz' 'python2-pytz')
noextract=("core-28.zip")
#source=("https://pypi.python.org/packages/source/B/Babel/Babel-$pkgver.tar.gz"
source=("$pkgbase-$pkgver.tar.gz::https://github.com/python-babel/babel/archive/v$pkgver.tar.gz"
	"core-29.zip::http://unicode.org/Public/cldr/29/core.zip")
sha256sums=('5022706550b92f504ff10acc488890490a8800268b15240a475aa2b5f107e35c'
            'b3308f8d3b4a80045ce4262b2784ac8d99775e80aaacafbf1277833f6b28ffda')

prepare() {
  cd "$srcdir"/babel-${pkgver}
  mv "$srcdir"/core-29.zip cldr/
}

package_python-babel() {
  depends=('python' 'python-pytz')

  cd "$srcdir"/babel-${pkgver}
  python3 setup.py import_cldr
  python3 setup.py install --root="$pkgdir"
  install -D -m0644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_python2-babel() {
  depends=('python2' 'python2-pytz')

  cd "$srcdir"/babel-${pkgver}
  python2 setup.py import_cldr
  python2 setup.py install --root="$pkgdir"
  mv "$pkgdir"/usr/bin/pybabel "$pkgdir"/usr/bin/pybabel2
  install -D -m0644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
