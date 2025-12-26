# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
#     <tallero@0x6ec7cC56dCeC0a00CB15E97C64B1a5Ec7A31403c>

_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
_os="$(
  uname \
    -o)"
if [[ ! -v "_git" ]]; then
  _git="true"
fi
if [[ ! -v "_offline" ]]; then
  _offline="false"
fi
if [[ ! -v "_git_service" ]]; then
  if [[ "${_evmfs}" = "true" ]]; then
    _git_service="gitlab"
  elif [[ "${_evmfs}" = "false" ]]; then
    _git_service="github"
  fi
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _archive_format="zip"
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _archive_format="tar.gz"
    fi
  fi
fi
_pep517='true'
_py="python"
_pyver="$(
  "${_py}" \
    -V |
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$((
  ${_pyminver} + 1))"
_pkg=aiohttp-retry
_Pkg=aiohttp_retry
pkgname="${_py}-${_pkg}"
pkgver=2.8.3
_bundle_commit="1a3bc19e15de202755e5cdf67c1c011aef2926c9"
_commit="c5e6bb74b5373650527bc1f5c29ba5ad145dea48"
pkgrel=3
pkgdesc='Simple retry client for aiohttp.'
_http="https://${_git_service}.com"
if [[ "${_git_service}" == "github" ]]; then
  _ns='inyutin'
elif [[ "${_git_service}" == "gitlab" ]]; then
  _ns="themartiancompany"
fi
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
  "${_py}"
  "${_py}-setuptools"
  "${_py}-wheel"
)
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
  )
fi
if [[ "${_pep517}" == true ]]; then
  makedepends+=(
    "${_py}-build"
    "${_py}-installer"
  )
fi
checkdepends=(
  "${_py}-pytest"
  "${_py}-pytest-cov"
  "${_py}-pytest-xdist"
)
source=()
sha256sums=()
_url="${url}"
_tag="${_commit}"
_tag_name="commit"
_tarname="${pkgname}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
if [[ "${_offline}" == "true" ]]; then
  _url="file://${HOME}/${pkgname}"
fi
_gitlab_sum="SKIP"
_gitlab_sig_sum="SKIP"
_github_sum='SKIP'
_github_sig_sum="SKIP"
_bundle_sum="184c34e6a04c24da8928f6db2a9aef1fa6c3773ac3a34cd19977360e819b4fb9"
_bundle_sig_sum="52e0b723c1cc92eb13b10988ad4d1adc9c042f68ae8b3e159593e0e69270c850"
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _sum="${_bundle_sum}"
    _sig_sum="${_bundle_sig_sum}"
  fi
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _sum="SKIP"
    _sig_sum="SKIP"
  fi
fi
# Dvorak
_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
# Tallero
_evmfs_ns="0x6ec7cC56dCeC0a00CB15E97C64B1a5Ec7A31403c"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_sig_uri="${_evmfs_dir}/${_sig_sum}"
_sig_src="${_tarfile}.sig::${_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  _src="${_evmfs_src}"
  source+=(
    "${_sig_src}"
  )
  sha256sums+=(
    "${_sig_sum}"
  )
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == true ]]; then
    _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
    _sum="SKIP"
  elif [[ "${_git}" == false ]]; then
    _uri=""
    if [[ "${_git_service}" == "github" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/archive/${_commit}.${_archive_format}"
        _sum="${_github_sum}"
      fi
    elif [[ "${_git_service}" == "gitlab" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/-/archive/${_tag}/${_tag}.${_archive_format}"
      fi
    fi
    _src="${_tarfile}::${_uri}"
  fi
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)
validpgpkeys=(
  # Truocolo
  #   <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
  #   <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
  'F690CBC17BD1F53557290AF51FC17D540D0ADEED'
  # Pellegrino Prevete (dvorak)
  #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

_git_unbundle() {
  local \
    _tarname="${1}" \
    _module \
    _bundle \
    _repo \
    _msg=()
  _bundle="${srcdir}/${_tarname}.bundle"
  _repo="${srcdir}/${_tarname}"
  _msg=(
    "Cloning '${_bundle}' into '${_repo}'."
  )
  msg \
    "${_msg[*]}"
  git \
    clone \
      "${_bundle}" \
      "${_repo}" || \
  git \
    -C \
      "${_repo}" \
      pull || \
    true
}

prepare() {
  if [[ "${_evmfs}" == "true" ]]; then
    if [[ "${_git}" == "true" ]]; then
      _git_unbundle \
        "${_tarname}"
    fi
  fi
}

build() {
  local \
    _build_opts=()
  _build_opts+=(
    --wheel
    --no-isolation
  )
  cd \
    "${_tarname}"
  export \
    LANG="en_US.UTF-8"
  if [[ "${_pep517}" == 'true' ]]; then
    "${_py}" \
      -m \
        build \
      "${_build_opts[@]}"
  elif [[ "${_pep517}" == 'false' ]]; then
    LANG="en_US.UTF-8" \
    "${_py}" \
      "setup.py" \
        build
  fi
}

check() {
  cd \
    "${_tarname}"
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
  local \
    _install_opts=() \
    _installer_opts=()
  _install_opts+=(
    --root="${pkgdir}"
    -O1
    --skip-build
  )
  _installer_opts+=(
    --destdir="${pkgdir}"
  )
  cd \
    ${_Pkg}-${pkgver}
  if [[ "${_pep517}" == 'false' ]]; then
    LANG="en_US.UTF-8" \
    "${_py}" \
      setup.py \
        install \
          "${_install_opts[@]}"
  elif [[ "${_pep517}" == 'true' ]]; then
    export \
      LANG="en_US.UTF-8"
    "${_py}" \
      -m \
        installer \
      "${_installer_opts[@]}" \
      "dist/"*".whl"
  fi
}

# vim: ts=2 sw=2 et:
