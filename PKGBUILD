# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Morten Linderud <foxboron@archlinux.no>
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor : Giedrius Slavinskas <giedrius25@gmail.com>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=babel
pkgname="${_py}-${_pkg}"
pkgver=2.14.0
# See the number here
# https://github.com/python-babel/babel/blob/master/scripts/download_import_cldr.py#L13
_core=43
pkgrel=2
pkgdesc="A collection of tools for internationalizing Python applications"
url="http://${_pkg}.pocoo.org/"
license=(
  "BSD"
)
arch=(
  'any'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-pytz"
)
makedepends=(
  "${_py}-setuptools"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-freezegun"
)
noextract=(
  "cldr-core-$_core.zip"
)
_http="https://github.com"
_ns="${pkgname}"
_url="${_http}/${_ns}/${_pkg}"
source=(
  "${_pkg}-${pkgver}.tar.gz::${_url}/archive/v${pkgver}.tar.gz"
  "cldr-core-${_core}.zip::http://unicode.org/Public/cldr/${_core}/core.zip"
  "cldr-common-${_core}.0.zip::http://unicode.org/Public/cldr/${_core}/cldr-common-${_core}.0.zip"
)
sha256sums=(
  'ad76eab6905b626d7d4110d2032bc60c69bef225ec94c67d7229425ebe53f659'
  '7800dadb6a11e06ba1475f8c2830aa87e0749ed441c953d8deea60b4baeef592'
  '7800dadb6a11e06ba1475f8c2830aa87e0749ed441c953d8deea60b4baeef592'
)

prepare() {
  cp \
    "${srcdir}/cldr-core-${_core}.zip" \
    "babel-${pkgver}/cldr/cldr-core-${_core}.zip"
  cp \
    "${srcdir}/cldr-common-${_core}.0.zip" \
    "babel-${pkgver}/cldr/cldr-common-${_core}.0.zip"
}

build(){
  cd \
    "${_pkg}-$pkgver"
  "${_py}" \
    setup.py \
      import_cldr
  "${_py}" \
    setup.py \
      build
}

check(){
  cd \
    "${_pkg}-$pkgver"
  # the tests fail if running in the wrong timezone:
  # https://github.com/python-babel/babel/issues/757
  TZ=UTC \
  pytest \
    -k \
      'not test_setuptools_commands'
}

package_python-babel() {
  cd \
    "${_pkg}-$pkgver"
  "${_py}" \
    setup.py \
      install \
        --root="${pkgdir}" \
	--optimize=1 \
	--skip-build
  install \
    -Dm0644 \
    LICENSE \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
