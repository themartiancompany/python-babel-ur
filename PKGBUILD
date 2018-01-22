# Maintainer: Morten Linderud <foxboron@archlinux.no> 
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor : Giedrius Slavinskas <giedrius25@gmail.com>

pkgbase=python-babel
pkgname=(python-babel python2-babel)
pkgver=2.5.3
pkgrel=3
pkgdesc="A collection of tools for internationalizing Python applications"
url="http://babel.pocoo.org/"
license=("BSD")
arch=('any')
makedepends=('python' 'python2'
	    'python-setuptools' 'python2-setuptools'
	    'python-pytz' 'python2-pytz')
noextract=("core-28.zip")
source=("$pkgbase-$pkgver.tar.gz::https://github.com/python-babel/babel/archive/v$pkgver.tar.gz"
	"core-29.zip::http://unicode.org/Public/cldr/29/core.zip")
sha256sums=('4c231f28875552abe18c6c10829cec0884d7eeb27423b562357250dc32090cb9'
            'b3308f8d3b4a80045ce4262b2784ac8d99775e80aaacafbf1277833f6b28ffda')

prepare() {
  cp -a babel-$pkgver{,-py2}
  cp "$srcdir"/core-29.zip babel-$pkgver-py2/cldr/
  cp "$srcdir"/core-29.zip babel-$pkgver/cldr/
}

build(){
  cd "$srcdir/babel-$pkgver"
  python setup.py build
  python setup.py import_cldr

  cd "$srcdir/babel-$pkgver-py2"
  python2 setup.py build
  python2 setup.py import_cldr
}

package_python-babel() {
  depends=('python' 'python-pytz')

  cd "$srcdir"/babel-${pkgver}
  python setup.py install --root="$pkgdir" --optimize=1 --skip-build
  mv babel/locale-data "$pkgdir"/usr/lib/python3.6/site-packages/babel/
  install -D -m0644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_python2-babel() {
  depends=('python2' 'python2-pytz')

  cd "$srcdir"/babel-${pkgver}-py2
  python2 setup.py install --root="$pkgdir" --optimize=1 --skip-build
  mv babel/locale-data "$pkgdir"/usr/lib/python2.7/site-packages/babel/
  mv "$pkgdir"/usr/bin/pybabel "$pkgdir"/usr/bin/pybabel2
  install -D -m0644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
