# Maintainer: Daniel Micay <danielmicay@gmail.com>

pkgname="sqlite4-fossil"
pkgver=20120817
pkgrel=1
pkgdesc="A C library that implements an SQL database engine"
arch=('i686' 'x86_64')
license=('custom')
url="http://www.sqlite.org/"
makedepends=('tcl' 'readline' 'fossil')
options=('!libtool' '!emptydirs')

_gitroot=GITURL
_gitname=MODENAME

build() {
  export CFLAGS="$CFLAGS -DSQLITE_ENABLE_FTS3=1 -DSQLITE_ENABLE_COLUMN_METADATA=1 -DSQLITE_ENABLE_UNLOCK_NOTIFY -DSQLITE_SECURE_DELETE"

  if [[ -f sqlite4.fossil ]]; then
    fossil pull http://www.sqlite.org/src4/ -R sqlite4.fossil
  else
    fossil clone http://www.sqlite.org/src4/ sqlite4.fossil
  fi

  rm -rf sqlite4-build
  mkdir sqlite4-build
  cd sqlite4-build
  fossil open ../sqlite4.fossil

  ln -s GNUmakefile.linux GNUmakefile

  make
}

package() {
  cd $srcdir/sqlite4-build

  install -Dm755 sqlite4 $pkgdir/usr/bin/sqlite4
  install -Dm644 libsqlite4.a $pkgdir/usr/lib/libsqlite4.a
  install -Dm644 sqlite4.h $pkgdir/usr/include/sqlite4.h
}
