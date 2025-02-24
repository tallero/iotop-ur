# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2025  Pellegrino Prevete
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

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer: Jaroslav Lichtblau <svetlemodry@archlinux.org>
# Contributor: Emmanuel Gil Peyrot <linkmauve@linkmauve.fr>


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
_pkg=iotop
pkgname="${_pkg}"
pkgver=0.6
pkgrel=12
pkgdesc='View I/O usage of processes'
arch=(
  'any'
)
_http="https://guichaz.free.fr"
_ns="${_pkg}"
url="${_http}/${_ns}"
license=(
  'GPL'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-wheel"
)
provides=(
  "${_py}-${_pkg}=${pkgver}"
)
changelog="${_pkg}.changelog"
_url="${url}/files"
_tarname="${_pkg}-${pkgver}"
source=(
  "${_url}/${_tarname}.tar.bz2"{"",".asc"}
)
sha256sums=(
  '3adea2a24eda49bbbaeb4e6ed2042355b441dbd7161e883067a02bfc8dcef75b'
  'SKIP'
)
validpgpkeys=(
  # Guillaume Chazarain <guichaz@gmail.com>
  '72FCCF352015B102B5E60D31959E7A3E4D23A27E'
)
prepare() {
  cd \
    "${srcdir}/${_tarname}"
  # Install binary to /usr/bin
  sed \
    -i \
      '7,13d' \
    "setup.py"
}

build() {
  cd \
    "${srcdir}/${_tarname}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

package() {
  cd \
    "${srcdir}/${_tarname}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    "dist/"*".whl"
  #FS#33906 fix
  chmod \
    644 \
    "${pkgdir}/usr/share/man/man8/iotop.8"
}
