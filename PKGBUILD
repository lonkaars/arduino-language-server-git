# Maitainer: Loek Le Blansch <loek@pipeframe.xyz>

pkgname=arduino-language-server-git
pkgver=r239.134ca4d
pkgrel=1
pkgdesc="An Arduino Language Server based on Clangd to Arduino code autocompletion"
arch=(x86_64 i686 i486 pentium4 arm armv6h armv7h aarch64)
url="https://github.com/arduino/arduino-language-server"
license=('Apache')
makedepends=('git' 'go')
provides=('arduino-language-server')
conflicts=('arduino-language-server')
source=(git+https://github.com/arduino/arduino-language-server)
sha256sums=('SKIP')

pkgver() {
  cd "${pkgname%-git}"
  ( set -o pipefail
    git describe --long 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

build() {
  cd "${pkgname%-git}"
  go build \
    -trimpath \
    -buildmode=pie \
    -mod=readonly \
    -modcacherw \
    -ldflags "-linkmode external -extldflags \"${LDFLAGS}\"" \
    .
}

package() {
  cd "${pkgname%-git}"
  install -Dm 755 arduino-language-server -t "$pkgdir"/usr/bin
}
