# Maintainer: SeeLook <seelook@gmail.com>
pkgname=nootka-hg
_pkgname=nootka
pkgver=2150
pkgrel=2
pkgdesc="Developing version of open-source application to help with learning classical score notation."
arch=('i686' 'x86_64')
url="http://${_pkgname}.sourceforge.net/"
license=('GPL')
depends=('qt5-base' 'qt5-svg' 'fftw' 'shared-mime-info' 'libvorbis' 'soundtouch')
optdepends=('libpulse: for PulseAudio' 'libjack: for JACK')
conflicts=('nootka')
makedepends=('mercurial' 'cmake' 'qt5-base' 'qt5-svg' 'fftw' 'libvorbis' 'soundtouch')
install="${pkgname}.install"

_hgroot="http://hg.code.sf.net/p/${_pkgname}/hg/"
_hgrepo="${_pkgname}"

build() {
  cd "${srcdir}"
  msg2 "Connecting to Mercurial server...."
  if [ -d ${_hgrepo} ] ; then
    cd ${_hgrepo} && hg pull -u
    msg2 "Local files are up to date."
  else
    hg clone ${_hgroot} ${_hgrepo}
  fi
  msg2 "Mercurial checkout done or server timeout."
  if [[ -d "${srcdir}/${_pkgname}/build" ]]; then
    msg2 "Cleaning the previous build directory..."
    rm -rf "${srcdir}/${_pkgname}/build"
  fi
  mkdir -p "${srcdir}/${_pkgname}/build"
  cd "${srcdir}/${_pkgname}/build"
  cmake .. -DCMAKE_INSTALL_PREFIX='/usr'
}

package() {
  cd "${srcdir}/${_pkgname}/build"
  make DESTDIR="${pkgdir}" install
}
