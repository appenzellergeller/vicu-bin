# Maintainer: Aurelio Bachmann <aurelio.bachmann@outlook.com>
pkgname=vicu-bin
pkgver=1.8.0
pkgrel=1
pkgdesc="Task management desktop app powered by Vikunja (prebuilt AppImage)"
arch=('x86_64' 'aarch64')
url="https://github.com/rendyhd/Vicu"
license=('MIT')
depends=('gtk3' 'nss' 'alsa-lib' 'libxss' 'libxtst' 'at-spi2-core' 'libdrm' 'mesa'
	'xdg-utils' 'hicolor-icon-theme' 'fuse2')
provides=('vicu')
conflicts=('vicu')
options=('!strip')
source_x86_64=("vicu.AppImage::https://github.com/rendyhd/Vicu/releases/download/v${pkgver}/Vicu-${pkgver}-x86_64.AppImage")
source_aarch64=("vicu.AppImage::https://github.com/rendyhd/Vicu/releases/download/v${pkgver}/Vicu-${pkgver}-arm64.AppImage")
source=('vicu.desktop' 'vicu.png')
sha256sums=('066ba342fe45a5a6f0730040d219f3d464ac131728ef803d82beb520d33200da'
	'c12f96dd2ec1286a08148cf9055ac79093050590d3bf70b7a4c9e0110bd1cb80')
sha256sums_x86_64=('ebab70d32e794b6951a7e2a1d6ce07a13c50aa4d6d6383a2529c15dca11b3ced')
sha256sums_aarch64=('8b2c37588efd73c0e462147d544f05237a21bbf51661d6e91ffb3f16e9562fe3')

package() {
	install -Dm755 "$srcdir/vicu.AppImage" "$pkgdir/opt/$pkgname/vicu.AppImage"

	install -Dm755 /dev/stdin "$pkgdir/usr/bin/vicu" <<EOF
#!/bin/sh
exec /opt/$pkgname/vicu.AppImage "\$@"
EOF

	install -Dm644 "$srcdir/vicu.desktop" "$pkgdir/usr/share/applications/vicu.desktop"
	install -Dm644 "$srcdir/vicu.png" "$pkgdir/usr/share/icons/hicolor/512x512/apps/vicu.png"
}
