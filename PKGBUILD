# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>

_py="python"
_pkg=gyp
pkgname="${_pkg}"
pkgver=20230914.a03d7413
pkgrel=2
pkgdesc="Generate Your Projects meta-build system"
url="https://${_pkg}.gsrc.io/"
arch=(
  any
)
license=(
  custom:BSD
)
depends=(
  ninja
  "${_py}-six"
)
makedepends=(
  git
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-wheel"
)
provides=(
  "${_py}-${_pkg}"
)
_commit=a03d7413becefc8d55c8aa3df58b55b9bd0e9052  # changes/05/4858505/3
source=(
  "git+https://chromium.googlesource.com/external/${_pkg}#commit=$_commit"
  "0001-${_pkg}-python38.patch"
  "0002-${_pkg}-fix-cmake.patch"
  "0003-${_pkg}-fips.patch"
)
b2sums=(
  'SKIP'
  '639848a0f0eb26bc16304b9c1ef2944f5cf37b2d7367a7de34becf2ec0962ce43820a21cd6c4d839775fc2dc1440c6e94f10cfd7781c5fe2278ba497b3fbdcb9'
  'f77bda072b6a3916c78c2061ceffa8b17bf1341d13509089effd3961e22cb315f68fdf749ab4a6abea37a9ecd61989ddcd75229a45d026e068bf11037ad4499c'
  '61febe5fb8672c2ad4012957b1f42d2909b7adae9b9c62417c22073b7d97dfad37cb34c19839b13bea54f8ab45c068f7b121bd3b4ae62d5234611861cae73c98'
)

pkgver() {
  local \
    _commit_date \
    _short_rev
  cd \
    "${_pkg}"
  _commit_date="$( \
    TZ=UTC \
    git \
      show \
      -s \
        --pretty=%cd \
        --date=format-local:%Y%m%d \
        HEAD)"
  _short_rev="$( \
    git \
      rev-parse \
        --short \
        HEAD)"
  echo \
    "${_commit_date}.${_short_rev}"
}

prepare() {
  cd \
    "${_pkg}"
  # Python 3 fixes from Fedora
  git \
    apply \
    -3 \
    ../*.patch
}

build() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

package() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dt \
    "${pkgdir}/usr/share/licenses/${pkgname}" \
    -m644 \
    LICENSE
}

# vim:set sw=2 sts=-1 et:
