# Maintainer: Paul <paul@mrarm.io>
pkgname=mcpelauncher-linux-git
pkgver=v0.2
pkgrel=1
pkgdesc="Minecraft: Pocket Edition launcher for Linux (Fork)"
arch=('x86_64' 'i686')
url="https://github.com/ChristopherHX/mcpelauncher-manifest"
license=('GPL3' 'custom')
makedepends_x86_64=('git' 'cmake' 'gcc-multilib')
makedepends_i686=('git' 'cmake' 'gcc')
depends_x86_64=('lib32-curl' 'lib32-libx11' 'lib32-zlib' 'lib32-libpng' 'lib32-libevdev' 'lib32-systemd' 'lib32-libxi' 'lib32-libegl')
depends_i686=('curl' 'libx11' 'zlib' 'libpng' 'libevdev' 'systemd' 'libxi' 'libegl')
optdepends=('mcpelauncher-msa: Xbox Live support')
provides=('mcpelauncher-client' 'mcpelauncher-server')
conflicts=('mcpelauncher-client' 'mcpelauncher-server')
source=(
  'git://github.com/ChristopherHX/mcpelauncher-manifest.git'
  'nlohmann_json_license.txt::https://raw.githubusercontent.com/nlohmann/json/develop/LICENSE.MIT'
)
md5sums=(
  'SKIP'
  'SKIP'
)

pkgver() {
  cd mcpelauncher-manifest
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}
prepare() {
  cd mcpelauncher-manifest
  git remote https://github.com/ChristopherHX/mcpelauncher-manifest.git
  git remote get-url origin
  git remote set-url origin
  git submodule init
  git submodule update
}
build() {
  cd mcpelauncher-manifest
  mkdir -p build
  cd build
  cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=RelWithDebInfo -DENABLE_DEV_PATHS=OFF ..
  make -j16
}
package() {
  cd mcpelauncher-manifest/build
  make -j16 DESTDIR="$pkgdir" install

  install -Dm644 ../LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 ../msa-daemon-client/LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE.MIT"
  install -Dm644 ../mcpelauncher-linux-bin/FMod\ License.txt "$pkgdir/usr/share/licenses/$pkgname/fmod_license.txt"
  install -Dm644 ../libhybris/LICENSE "$pkgdir/usr/share/licenses/$pkgname/libhybris_license.txt"
  install -Dm644 ../eglut/LICENSE "$pkgdir/usr/share/licenses/$pkgname/eglut_license.txt"
  install -Dm644 ../../nlohmann_json_license.txt "$pkgdir/usr/share/licenses/$pkgname/nlohmann_json_license.txt"
}
