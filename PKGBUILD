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
#   cp $srcdir/$pkgname-$pkgver/config.def.h ../../config.h
   cd "$srcdir/$pkgname-$pkgver"

 for p in "${_patches[@]}"; do
    echo "=> $p"
    patch < ../$p || return 1
  done

   cp $srcdir/$pkgname-$pkgver/config.def.h $srcdir/$pkgname-$pkgver/config.h
}

build() {
  cd "$srcdir/$pkgname-$pkgver"


#  for p in "${_patches[@]}"; do
#    echo "=> $p"
#    patch < ../$p || return 1
#  done

#  cp $srcdir/config.h config.h


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
         '2453e037f46449774ec8afab49b4f1a2'
         '54fa01e890334d2583d1a1d1285311dc'
         '935b9d740b375ba2ebd7498417072f8a'
         'af2f17b35dfb332a71f34210074c802f'
         'f93898086ea4d336bb75bf8eccfed311'
         'bb2c985629f6255add95a25d41417fd5'
         '55bb2b7d43df438f2b5cffaf703f3d14')
