# Maintainer: Kuba Serafinowski <zizzfizzix(at)gmail(dot)com>
# https://github.com/zizzfizzix/pkgbuilds

##############################################################
#### The section below can be adjusted to suit your needs ####
##############################################################

# What type of build do you want?
# See http://techbase.kde.org/Development/CMake/Addons_for_KDE#Buildtypes to check what is supported.
# Default is RelWithDebInfo to help with debugging.

_buildtype="RelWithDebInfo"

##############################################################

pkgname=tomahawk
pkgver=0.6.0
pkgrel=1
pkgdesc="A Music Player App written in C++/Qt"
arch=('i686' 'x86_64')
url="http://tomahawk-player.org/"
license=('GPL3')
depends=('phonon' 'taglib' 'boost' 'clucene' 'libechonest2' 'jreen' 'qtweetlib' 'quazip' 'attica' 'qtwebkit' 'liblastfm')
makedepends=('git' 'cmake')
optdepends=('tomahawk-spotify-git: spotify resolver')
provides=('tomahawk')
conflicts=('tomahawk-git')
options=(!strip)
source=("http://download.tomahawk-player.org/${pkgname}-${pkgver}.tar.bz2")
sha256sums=('28ea3b1424a99879bf9457f04b3ce8e63dca9ee84e6651027a1ecad9d74ae335')

install=tomahawk.install

# Clean options array to strip pkg if release buildtype is chosen
if [[ ${_buildtype} == "Release" ]] || [[ ${_buildtype} == "release" ]]; then
  options=()
fi

build() {
  if [[ -e ${srcdir}/${pkgname}-${pkgver}-build ]]; then rm -rf ${srcdir}/${pkgname}-${pkgver}-build; fi
  mkdir ${srcdir}/${pkgname}-${pkgver}-build
  cd ${srcdir}/${pkgname}-${pkgver}-build

  cmake -DCMAKE_INSTALL_PREFIX=/usr \
        -DCMAKE_INSTALL_LIBDIR=lib \
        -DCMAKE_INSTALL_LIBEXECDIR=lib/${pkgname} \
        -DCMAKE_BUILD_TYPE=${_buildtype} \
        ../${pkgname}-${pkgver}
  make
}

package() {
  cd ${srcdir}/${pkgname}-${pkgver}-build
  make DESTDIR=${pkgdir} install
}
