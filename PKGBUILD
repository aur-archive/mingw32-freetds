pkgname=mingw32-freetds
pkgver=0.91
pkgrel=2
pkgdesc="Library for accessing Sybase and MS SQL Server databases (mingw32)"
url="http://www.freetds.org"
arch=(any)
license=("LGPL")
depends=(mingw32-runtime mingw32-libiconv)
makedepends=(mingw32-gcc)
conflicts=(mingw32-freetds-static)
provides=(mingw32-freetds-static)
options=(!strip !buildflags !libtool)
backup=("usr/i486-mingw32/etc/freetds.conf"
"usr/i486-mingw32/etc/locales.conf"
"usr/i486-mingw32/etc/pool.conf")
source=("ftp://ftp.ibiblio.org/pub/Linux/ALPHA/freetds/stable/freetds-stable.tgz")
md5sums=('b14db5823980a32f0643d1a84d3ec3ad')

build() {
  cd "$srcdir/freetds-$pkgver"
  unset LDFLAGS
  mkdir -p build && cd build
  ../configure \
    --prefix=/usr/i486-mingw32 \
    --host=i486-mingw32 \
    --enable-sybase-compat \
    --enable-static \
    --enable-shared \
    --with-tdsver=8.0 \
    --enable-threadsafe \
    --disable-debug \
    --enable-msdblib
  make
}

package() {
  cd "$srcdir/freetds-$pkgver/build"
  make DESTDIR=$pkgdir install
  rm -rf "$pkgdir/usr/i486-mingw32/share"
  i486-mingw32-strip $pkgdir/usr/i486-mingw32/bin/*.exe
  i486-mingw32-strip -x $pkgdir/usr/i486-mingw32/bin/*.dll
  i486-mingw32-strip -g $pkgdir/usr/i486-mingw32/lib/*.a
}
