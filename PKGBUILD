# Maintainer: Nicolas Hafner <shinmera@tymoon.eu>
pkgname="externals-clasp-git"
pkgver=35ac32f
pkgrel=1
_srcname="externals-clasp"
pkgdesc="Specific versions of libraries required to build Clasp"
arch=("x86_64")
url="https://github.com/drmeister/externals-clasp"
license=("LGPL2.1")
options=("libtool" "staticlibs" "!strip" "!makeflags" "!buildflags" "!distcc" "!ccache")
provides=("externals-clasp")
conflicts=("externals-clasp")
depends=("llvm>=3.6" "clang>=3.6" "boost>=1.55" "gc>=7.2" "gmp>=6.0.0" "expat>=2.0.1" "zlib>=1.2.8" "readline>=6.2")
makedepends=("gcc>=4.8" "perl")
source=("${_srcname}::git+https://github.com/drmeister/externals-clasp.git")
## In case you have a local copy and don't want to wait for the clone every time:
#source=("${_srcname}::git+file:///opt/clasp/package/externals-clasp/origin/")
sha256sums=("SKIP")

_make (){
    env -i HOME="$HOME" LC_CTYPE="${LC_ALL:-${LC_CTYPE:-$LANG}}" PATH="$PATH:/usr/bin/core_perl/" USER="$USER" make $1
}

pkgver() {
    cd "${srcdir}/${_srcname}"
    echo $(git rev-parse --short HEAD)
}

prepare() {
    local CPUS=$(grep -c '^processor' /proc/cpuinfo)
    cd "${srcdir}/${_srcname}"
    cat >local.config <<EOF
export TARGET_OS = linux
export PJOBS = $CPUS
export GCC_TOOLCHAIN = /usr
export TOOLSET = gcc
EOF
}

build() {
    cd "${srcdir}/${_srcname}"
    _make
}

package() {
    mkdir -p "${pkgdir}/opt/clasp/externals/"
    cp -r "${srcdir}/${_srcname}/build" "${pkgdir}/opt/clasp/externals/"
}
