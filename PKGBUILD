# Maintainer: gulaghad <can6dev <AT> gmail <DOT> com>
pkgname=tmx-parser-svn
pkgver=56
pkgrel=2
pkgdesc="Library for parsing TMX files (Tiled Maps) using TinyXML's DOM interface."
url='https://code.google.com/p/tmx-parser/'
license=('BSD')
depends=('tinyxml' 'zlib')
makedepends=('svn')
arch=('i686' 'x86_64')
options=('staticlibs')

_svnmod=tmx-parser
_svntrunk="http://tmx-parser.googlecode.com/svn/trunk/"

build() {
  cd ${srcdir}
  msg "Connecting to SVN server...."
  if [ -d ${_svnmod}/.svn ]; then
    msg "Updating tmx-parser SVN..."
    svn up ${_svnmod}
  else
    msg "Checking out tmx-parser SVN..."
    svn co ${_svntrunk} ${_svnmod}
  fi
  msg "SVN checkout done or server timeout."

  msg "Building tmx-parser..."
  cd ${_svnmod}
  make -f Makefile.linux
}

package() {
  cd ${srcdir}/${_svnmod}
  make -f Makefile.linux DESTDIR=${pkgdir} install
  chmod 644 ${pkgdir}/usr/lib/libtmxparser.a
  install -m 644 -D LICENSE ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
}
