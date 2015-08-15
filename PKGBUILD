# Maintainer: Moritz Maxeiner <moritz@ucworks.org>

pkgname=comp-scale-svn
pkgver=84104
pkgrel=1
pkgdesc="Enlightenment e17 module: Scale windows down to see them all. Side by side. Latest svn version for use with enlightenment17-svn, aka e18 development cycle"
arch=('i686' 'x86_64')
url="http://svn.enlightenment.org/svn/e/trunk/E-MODULES-EXTRA/comp-scale/"
license=('MIT')
depends=('enlightenment17-svn')
makedepends=('subversion')
provides=('comp-scale')
options=('!libtool')
source=()
conflicts=('e-modules-extra' 'comp-scale')

_svntrunk=http://svn.enlightenment.org/svn/e/trunk/E-MODULES-EXTRA/comp-scale/
_svnmod=comp-scale

build() {
  cd "$srcdir"

  msg "Connecting to SVN server...."
  if [ -d "$_svnmod/.svn" ]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"

  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  ./autogen.sh --prefix=/usr
  make
}

package() {
  cd "$srcdir/$_svnmod-build"
  make DESTDIR="$pkgdir/" install

  install -D -m644 COPYING $pkgdir/usr/share/licenses/$pkgname/COPYING
  install -D -m644 COPYING-PLAIN $pkgdir/usr/share/licenses/$pkgname/COPYING-PLAIN
}
