pkgname=dwm-jbal
_pkgname=dwm
pkgver=6.2.r19.ga69be4c
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
depends=('libx11' 'libxinerama' 'libxft-bgra' 'freetype2' 'st' 'dmenu')
makedepends=('git')
provides=('dwm')
conflicts=('dwm')
source=("$pkgname::git+file:///home/jbal/Documents/dwm"
        "dwm.desktop")
sha256sums=('SKIP' 'SKIP')

pkgver(){
  cd $pkgname
  git describe --long --tags | sed -E 's/([^-]*-g)/r\1/;s/-/./g'
#  #printf "%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd "$srcdir/$pkgname" 
  if [[ -f "$srcdir/config.h" ]]; then
    cp -fv "$srcdir/config.h" config.h
  fi
}

build() {
  cd "$srcdir/$pkgname"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd "$srcdir/$pkgname"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -m644 -D README "$pkgdir/usr/share/doc/$pkgname/README"
  install -m644 -D "$srcdir/dwm.desktop" "$pkgdir/usr/share/xsessions/dwm.desktop"
}

# vim:set ts=2 sw=2 et:
