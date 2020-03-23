# Maintainer: Ryan Scott Lewis <ryanscottlewis@gmail.com>

pkgname=lightbar-git
_gitname=lightbar-rb
_gemname=lightbar
_gemversion=0.0.1
pkgver=20200323.r34.eb8945c
pkgrel=1
pkgdesc='Lightbar PWM Tweening Controller'

arch=('any')
url="https://github.com/RyanScottLewis/lightbar-rb"
license=('MIT')

depends=(ruby ruby-dbus)
optdepends=("pi-blaster-git: PWM support")
source=("git+https://github.com/RyanScottLewis/${_gitname}")
sha256sums=('SKIP')
install=$pkgname.install

pkgver() {
  cd "$_gitname"
  ( set -o pipefail
    git describe --long 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "%s.r%s.%s" "$(date +%Y%m%d)" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

build() {
  cd "$_gitname"
  make
}

package() {
  local _gemdir="$(ruby -e'puts Gem.default_dir')"
  local _rootdir="$pkgdir/$_gemdir/gems/$pkgname-$pkgver"

  cd "$_gitname"

  # TODO: Why not move into `make install` within lightbar-rb?
  gem install --ignore-dependencies --no-user-install -N -i "$pkgdir/$_gemdir" -n "$pkgdir/usr/bin" pkg/$_gemname-$_gemversion.gem
  make DESTDIR="$pkgdir" install
}

