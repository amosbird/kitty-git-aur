# Maintainer: Fabio 'Lolix' Loli <fabio.loli@disroot.org> -> https://github.com/FabioLolix
# Contributor: timescam <rex.ky.ng at gmail dot com>
# Contributor: Maximilian Kindshofer <maximilian@kindshofer.net>

pkgbase=kitty-git
pkgname=kitty-git
pkgver=99999.r12012
pkgrel=1
epoch=1
pkgdesc="Modern, hackable, featureful, OpenGL based terminal emulator"
arch=(i686 x86_64)
url="https://sw.kovidgoyal.net/kitty/"
license=(GPL3)
depends=(python freetype2 fontconfig wayland libx11 libxi libgl libcanberra dbus lcms2
         libxkbcommon-x11 librsync python-pygments ncurses)
makedepends=(git go python-setuptools libxinerama libxcursor libxrandr libxkbcommon mesa
             wayland-protocols python-sphinx python-sphinx-copybutton
             python-sphinx-inline-tabs python-sphinxext-opengraph python-sphinx-furo)
source=("git+https://github.com/amosbird/kitty.git")
sha256sums=('SKIP')

pkgver() {
  cd "${srcdir}/${pkgname%-git}"
  printf "99999.r%s.g%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cd "${srcdir}/${pkgname%-git}"
  python3 setup.py linux-package --update-check-interval=0
}

package_kitty-git() {
  optdepends=('imagemagick: viewing images with icat')
  provides=(kitty-git)
  conflicts=(kitty kitty-terminfo)

  cd "${srcdir}/${pkgname%-git}"

  cp -r linux-package "${pkgdir}"/usr

  install -Dm644 "${pkgdir}"/usr/share/icons/hicolor/256x256/apps/kitty.png "${pkgdir}"/usr/share/pixmaps/kitty.png

  rm -r "$pkgdir"/usr/share/terminfo
  rm -r "$pkgdir"/usr/lib/kitty/shell-integration

  install -Dm644 docs/generated/conf/kitty.conf "${pkgdir}"/usr/share/doc/${pkgname}/kitty.conf

  mkdir -p "$pkgdir/usr/share/terminfo"
  tic -x -o "$pkgdir/usr/share/terminfo" terminfo/kitty.terminfo

  mkdir -p "$pkgdir/usr/lib/kitty/"
  cp -r "shell-integration" "$pkgdir/usr/lib/kitty/"
}
