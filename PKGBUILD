# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Contributor: Michael Yeatts <mwyeatts@gmail.com>

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
_Pkg=typing_extensions
_pkg=typing-extensions
pkgname="${_py}-${_pkg}"
pkgver=4.9.0
pkgrel=1
pkgdesc='Backported and Experimental Type Hints for Python 3.8+'
arch=(
  any
)
_http="https://github.com"
_ns="python"
url="${_http}/${_ns}/${_pkg}"
license=(
  custom
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  git
  "${_py}-build"
  "${_py}-flit-core"
  "${_py}-installer"
)
checkdepends=(
  "${_py}-tests"
)
provides=(
  "${_py}-${_Pkg}"
)
conflicts=(
  "${_py}-${_Pkg}"
)
_tag=fc461d6faf4585849b561f2e4cbb06e9db095307
source=(
  "${_pkg}-${pkgver}::git+${url}.git#tag=${_tag}"
)
b2sums=(
  SKIP
)

pkgver() {
  cd \
    "${_pkg}-${pkgver}"
  git \
    describe \
    --tags
}

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --skip-dependency-check \
    --no-isolation
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      unittest \
    discover \
    src
}

package() {
  local \
    _site_packages
  _site_packages=$( \
    "${_py}" \
      -c \
        "import site; print(site.getsitepackages()[0])")
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -d \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  ln \
    -s \
    "${_site_packages}/${_Pkg}-${pkgver}.dist-info/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim: ts=2 sw=2 et:
