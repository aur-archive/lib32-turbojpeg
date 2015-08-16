_pkgbasename=turbojpeg
pkgname=lib32-$_pkgbasename
pkgver=1.2.1
pkgrel=1
pkgdesc="turbojpeg library from libjpeg-turbo (32-bit)"
arch=('x86_64')
url="http://www.libjpeg-turbo.org/About/TurboJPEG"
license=('GPL' 'custom')
depends=('lib32-glibc' $_pkgbasename)
makedepends=('nasm' gcc-multilib)
options=('!libtool')
source=(http://sourceforge.net/projects/libjpeg-turbo/files/$pkgver/libjpeg-turbo-$pkgver.tar.gz)
sha1sums=('a4992e102c6d88146709e8e6ce5896d5d0b5a361')

build() {
  cd "$srcdir/libjpeg-turbo-$pkgver"

  export CC="gcc -m32"
  export CXX="g++ -m32"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

  sed -i "s|NAFLAGS='-felf64 -DELF -D__x86_64__'|NAFLAGS='-felf32 -DELF -D__x86_64__'|" configure
  ./configure --prefix=/usr --with-jpeg8 --mandir=/usr/share/man --libdir=/usr/lib32 --without-simd
  make
}

package() {
  cd "$srcdir/libjpeg-turbo-$pkgver"

  make DESTDIR="$pkgdir/" install

  # only distribute libturbojpeg
  rm "$pkgdir"/usr/lib32/libj*

  rm -rf "${pkgdir}"/usr/{include,share,bin,sbin}
  mkdir -p "$pkgdir/usr/share/licenses"
  ln -s $_pkgbasename "$pkgdir/usr/share/licenses/$pkgname"
}
