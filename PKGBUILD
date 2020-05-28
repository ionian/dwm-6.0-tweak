pkgname=dwm
pkgver=6.0
pkgrel=2
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
    dwm.desktop
	config.h
    )
_patches=(01.Setup.makefiles.patch
          02.Base.config.changes.patch
          03.New.master.patch
          04.Xft.patch
          05.Statuscolours-config.h.patch
          07.Statuscolours-dwm.c.patch
          )
source=(${source[@]} ${_patches[@]})

prepare() {
   cd "$srcdir/$pkgname-$pkgver"

 for p in "${_patches[@]}"; do
    echo "=> $p"
    patch < ../$p || return 1
  done

}

build() {
   cd "$srcdir/$pkgname-$pkgver"
   cp -r "$srcdir/$pkgname-$pkgver/config.def.h" "$HOME/builds-arch/dwm/dwm-6.0-tweak/config.h"

  sed -i 's/CPPFLAGS =/CPPFLAGS +=/g' config.mk
  sed -i 's/^CFLAGS = -g/#CFLAGS += -g/g' config.mk
  sed -i 's/^#CFLAGS = -std/CFLAGS += -std/g' config.mk
  sed -i 's/^LDFLAGS = -g/#LDFLAGS += -g/g' config.mk
  sed -i 's/^#LDFLAGS = -s/LDFLAGS += -s/g' config.mk
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR=$pkgdir install
  install -m644 -D LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
  install -m644 -D README $pkgdir/usr/share/doc/$pkgname/README
  install -m644 -D $srcdir/dwm.desktop $pkgdir/usr/share/xsessions/dwm.desktop
}
md5sums=('8bb00d4142259beb11e13473b81c0857'
         '939f403a71b6e85261d09fc3412269ee'
         '7f3f580bace83adf93973b3fb6509736'
         '009a8b8f7c3b28414f9cd966678ce65c'
         'a845ac2cbec7512c6f515418f7554411'
         '7a6b8586127c7169ab2485cb89aeda42'
         'eb03fb0e8368e9f69a9d28271d73acc5'
         'bb2c985629f6255add95a25d41417fd5'
         '55bb2b7d43df438f2b5cffaf703f3d14')
