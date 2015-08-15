# Maintainer: speps <speps at aur dot archlinux dot org>

pkgname=gnoduino
pkgver=0.5.1
pkgrel=2
pkgdesc="An implementation of well-known Arduino IDE for GNOME"
arch=(any)
url="http://gnome.eu.org/index.php/Gnoduino"
license=('GPL')
depends=('avr-libc' 'avrdude' 'avr-binutils' 'avr-gcc' 'pyxdg'
         'pygtksourceview2' 'python2-pyserial'
         'python2-gconf' 'desktop-file-utils')
makedepends=('python2-distribute')
install="$pkgname.install"
source=("http://gnome.eu.org/$pkgname-$pkgver.tar.gz")
md5sums=('e458acd24860e28acec7fa71bb9cfe2f')

prepare() {
  cd $pkgname-$pkgver

  # do not install gconf schema
  sed -i "/installSchema.*)$/d" setup.py

  # python2 shebang
  sed -i "s|bin/python$|&2|" `find . -name "*.py"`
}

build() {
  cd $pkgname-$pkgver
  python2 setup.py build
}

package() {
  cd $pkgname-$pkgver
  python2 setup.py install --root="$pkgdir/"

  # gconf schema
  install -Dm644 data/$pkgname.schemas \
    "$pkgdir/usr/share/gconf/schemas/$pkgname.schemas"
}

# vim:set ts=2 sw=2 et:
