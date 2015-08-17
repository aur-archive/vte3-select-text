# Maintainer: Daniel Micay <danielmicay@gmail.com>
# Contributor: Ionut Biru <ibiru@archlinux.org>

pkgname=vte3-select-text
pkgver=0.40.2
pkgrel=1
pkgdesc="Virtual Terminal Emulator widget for use with GTK3"
arch=('i686' 'x86_64')
license=('LGPL')
options=('!libtool' '!emptydirs')
depends=('gtk3' 'vte-common')
makedepends=('intltool' 'gobject-introspection' 'gtk3' 'python2' 'vala')
url="http://www.gnome.org"
source=(http://download.gnome.org/sources/vte/${pkgver::4}/vte-$pkgver.tar.xz
        expose_select_text.patch)
sha256sums=('9b68fbc16b27f2d79e6271f2b0708808594ac5acf979d0fccea118608199fd2d'
            '929f8bc647215f1580cc176f816d8793c47d8076a7d5329f4145d2d6aec62b88')
provides=(vte3)
conflicts=(vte3)

prepare() {
  cd "vte-$pkgver"
  patch -p1 -i ../expose_select_text.patch
}

build() {
  cd "vte-$pkgver"
  ./configure --prefix=/usr --sysconfdir=/etc \
    --libexecdir=/usr/lib/vte \
    --localstatedir=/var --disable-static \
    --enable-introspection --enable-gnome-pty-helper
  make
}

package() {
  cd "vte-$pkgver"
  make DESTDIR="$pkgdir" install
  rm "$pkgdir/etc/profile.d/vte.sh"
  rm "$pkgdir/usr/lib/vte/gnome-pty-helper"
}
