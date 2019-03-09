# Maintainer:  Håvard Pettersson <mail@haavard.me>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Thorsten Töpper <atsutane-tu@freethoughts.de>
# Contributor: Thayer Williams <thayer@archlinux.org>
# Contributor: Jeff 'codemac' Mickey <jeff@archlinux.org>

_pkgname=dmenu
pkgname=$_pkgname-git
pkgver=4.9.5.gdb6093f
pkgrel=1
pkgdesc="A generic menu for X"
url="http://tools.suckless.org/dmenu/"
arch=('i686' 'x86_64')
license=('MIT')
depends=('sh' 'libxinerama' 'libxft')
makedepends=('git')
provides=($_pkgname)
conflicts=($_pkgname)
source=(git://git.suckless.org/$_pkgname dmenu.patch)
sha256sums=('SKIP'
            '8b0a685b984b77e35c1a53a4504e26d511bdaeb708399c7e6dc0f33f927b190a')

pkgver() {
  cd $_pkgname
  git describe --tags --long | sed 's/-/./g'
}

prepare() {
  cd $_pkgname
  patch --strip=1 --input=../dmenu.patch
  # to use a custom config.h, place it in the package directory
  if [[ -f ${SRCDEST}/config.h ]]; then
      cp "${SRCDEST}/config.h" .
  fi
}

build(){
  cd $_pkgname
  make \
    X11INC=/usr/include/X11 \
    X11LIB=/usr/lib/X11
}

package() {
  cd $_pkgname
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
