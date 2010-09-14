# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor : Giedrius Slavinskas <giedrius25@gmail.com>

pkgname=python-babel
pkgver=0.9.5
pkgrel=2
pkgdesc="A collection of tools for internationalizing Python applications"
url="http://babel.edgewall.org/"
license=("BSD")
arch=('any')
depends=('python2')
makedepends=('setuptools')
source=("http://ftp.edgewall.com/pub/babel/Babel-$pkgver.tar.gz")
md5sums=('05603f058644f81b9b5f75d0161a14dd')

build() {
  cd $srcdir/Babel-${pkgver}

  # python2 fix
  sed -i 's_#!/usr/bin/env python_#!/usr/bin/env python2_' babel/messages/frontend.py

  python2 setup.py install --root=$pkgdir
  install -D -m0644 COPYING $pkgdir/usr/share/licenses/$pkgname/COPYING
}
