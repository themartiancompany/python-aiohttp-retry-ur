# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>

_pep517='true'
_py="python"
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
_pkg=aiohttp-retry
_Pkg=aiohttp_retry
pkgname="${_py}-${_pkg}"
pkgver=2.8.3
pkgrel=1
pkgdesc='Simple retry client for aiohttp.'
_http='https://github.com'
_ns='inyutin'
url="${_http}/${_ns}/${_pkg}"
arch=(
  'x86_64'
  'arm'
  'aarch64'
  'armv7l'
  'i686'
  'pentium4'
  'powerpc'
  'mips'
)
license=(
  'MIT'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-aiohttp"
  "${_py}-yarl"
)
makedepends=(
  "${_py}-setuptools"
  "${_py}-wheel"
)
[[ "${_pep517}" == true ]] && \
  makedepends+=(
    "${_py}-build"
    "${_py}-installer"
  )
checkdepends=(
  "${_py}-pytest"
  "${_py}-pytest-cov"
  "${_py}-pytest-xdist"
)
source=(
  "${url}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz"
)
sha512sums=(
  '71869c3997e9b5089c298fa6f992b0ed08ca3da0f93c4f37566d8c6b9809bb1873a629cc47f1ffaeccac112d96036851794ee564b11c0f4f1eec00f49413358d'
)
b2sums=(
  'f2ea6f7b2f13001bd8d49b4529eacb3766cab080ff3a9457e40287bc797afebae10393a628cf78756074ca60a62df78c59c6120f1368316084155f1d7fd7cdfb'
)

prepare() {
  cd \
    "${_Pkg}-${pkgver}"
}

build() {
  cd \
    "${_Pkg}-${pkgver}"
  export \
    LANG="en_US.UTF-8"
  if [[ "${_pep517}" == 'true' ]]; then
    "${_py}" \
      -m \
        build \
      --wheel \
      --no-isolation
  elif [[ "${_pep517}" == 'false' ]]; then
    LANG="en_US.UTF-8" \
    "${_py}" \
      setup.py \
        build
  fi
}

check() {
  cd \
    "${_Pkg}-${pkgver}"
  "${_py}" \
    -m \
      venv \
    --system-site-packages \
    test-env
  test-env/bin/python \
    -m \
      installer \
    dist/*.whl
  cd \
    tests
  ../test-env/bin/"${_py}" \
    -m pytest \
    -v
}

package() {
  cd \
    ${_Pkg}-${pkgver}
  if [[ "${_pep517}" == 'false' ]]; then
    LANG="en_US.UTF-8" \
    "${_py}" \
      setup.py \
        install \
          --root="${pkgdir}" \
          -O1 \
          --skip-build
  elif [[ "${_pep517}" == 'true' ]]; then
    export \
      LANG="en_US.UTF-8"
    "${_py}" \
      -m \
        installer \
      --destdir="${pkgdir}" \
      dist/*.whl
  fi
}

# vim: ts=2 sw=2 et:
