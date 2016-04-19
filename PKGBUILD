# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor : Giedrius Slavinskas <giedrius25@gmail.com>

pkgbase=python-babel
pkgname=(python-babel python2-babel)
pkgver=2.3.3
pkgrel=1
pkgdesc="A collection of tools for internationalizing Python applications"
url="http://babel.pocoo.org/"
license=("BSD")
arch=('any')
makedepends=('python' 'python2'
	    'python-setuptools' 'python2-setuptools'
	    'python-pytz' 'python2-pytz')
noextract=("core-28.zip")
#source=("$pkgbase-$pkgver.tar.gz::https://github.com/mitsuhiko/babel/archive/$pkgver.tar.gz")
source=("https://pypi.python.org/packages/source/B/Babel/Babel-$pkgver.tar.gz"
	"core-28.zip::http://unicode.org/Public/cldr/28/core.zip")
md5sums=('7385ea5b37005f4b2015f971044431f6'
         'a4e9ee67b3545df299043164cd78fca1')

prepare() {
  cd $srcdir/Babel-${pkgver}
  mkdir cldr
  mv $srcdir/core-28.zip cldr/
}

package_python-babel() {
  depends=('python' 'python-pytz')

  cd $srcdir/Babel-${pkgver}
  python3 setup.py import_cldr
  python3 setup.py install --root=$pkgdir
  install -D -m0644 LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
}

package_python2-babel() {
  depends=('python2' 'python2-pytz')

  cd $srcdir/Babel-${pkgver}
  python2 setup.py import_cldr
  python2 setup.py install --root=$pkgdir
  mv $pkgdir/usr/bin/pybabel $pkgdir/usr/bin/pybabel2
  install -D -m0644 LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
}
