# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor : Giedrius Slavinskas <giedrius25@gmail.com>

pkgbase=python-babel
pkgname=(python-babel python2-babel)
pkgver=2.3.2
pkgrel=1
pkgdesc="A collection of tools for internationalizing Python applications"
url="http://babel.pocoo.org/"
license=("BSD")
arch=('any')
makedepends=('python' 'python2'
	    'python-setuptools' 'python2-setuptools'
	    'python-pytz' 'python2-pytz')
source=("$pkgbase-$pkgver.tar.gz::https://github.com/mitsuhiko/babel/archive/$pkgver.tar.gz")
md5sums=('8800dc94ba33bcd5e673b247de2eade2')

package_python-babel() {
  depends=('python' 'python-pytz')

  cd $srcdir/babel-${pkgver}
  python3 setup.py import_cldr
  python3 setup.py install --root=$pkgdir
  install -D -m0644 LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
}

package_python2-babel() {
  depends=('python2' 'python2-pytz')

  cd $srcdir/babel-${pkgver}
  python2 setup.py import_cldr
  python2 setup.py install --root=$pkgdir
  mv $pkgdir/usr/bin/pybabel $pkgdir/usr/bin/pybabel2
  install -D -m0644 LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
}
