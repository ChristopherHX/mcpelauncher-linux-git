# Maintainer: Paul <paul@mrarm.io>
pkgname=mcpelauncher-linux-git
pkgver=v0.3
pkgrel=1
pkgdesc="Minecraft: Pocket Edition launcher for Linux (ng)"
arch=('x86_64' 'i686')
url="https://github.com/minecraft-linux/mcpelauncher-manifest"
license=('GPL3' 'custom')
makedepends=('git' 'cmake' 'clang')
depends=('curl' 'libx11' 'zlib' 'libpng' 'libevdev' 'systemd' 'libxi' 'libegl')
optdepends=('mcpelauncher-msa: Xbox Live support' 'zenity: Select custom skins' 'alsa-lib: Audio via alsa' 'libpulse: Audio via pulseaudio')
provides=('mcpelauncher-client')
conflicts=('mcpelauncher-client')
source=(
  'git://github.com/minecraft-linux/mcpelauncher-manifest.git#branch=ng'
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
  git remote set-url origin https://github.com/minecraft-linux/mcpelauncher-manifest.git
  git submodule update --init --recursive
}
build() {
  cd mcpelauncher-manifest
  mkdir -p build
  cd build
  CC=clang CXX=clang++ cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=RelWithDebInfo -DENABLE_DEV_PATHS=OFF -DBUILD_FAKE_JNI_TESTS=OFF -DBUILD_FAKE_JNI_EXAMPLES=OFF ..
  make -j16
}
package() {
  cd mcpelauncher-manifest/build
  make -j16 DESTDIR="$pkgdir" install

  install -Dm644 ../LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 ../msa-daemon-client/LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE.MIT"
  install -Dm644 ../mcpelauncher-linux-bin/FMod\ License.txt "$pkgdir/usr/share/licenses/$pkgname/fmod_license.txt"
  install -Dm644 ../eglut/LICENSE "$pkgdir/usr/share/licenses/$pkgname/eglut_license.txt"
  install -Dm644 ../../nlohmann_json_license.txt "$pkgdir/usr/share/licenses/$pkgname/nlohmann_json_license.txt"
}
