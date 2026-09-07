_pkgname=stremio
pkgname=stremio-downmix-git
pkgver=4.4.183.r1.g28abc0d
pkgrel=1
pkgdesc="Stremio desktop client with multichannel dialogue downmixing"
arch=('x86_64')
url="https://www.stremio.com"
license=('MIT')
depends=('nodejs' 'ffmpeg' 'qt5-webengine' 'qt5-webchannel' 'qt5-declarative' 'qt5-quickcontrols' 'qt5-quickcontrols2' 'qt5-translations' 'mpv' 'openssl')
makedepends=('git' 'wget' 'qt5-tools' 'librsvg' 'cmake')
provides=('stremio')
conflicts=('stremio' 'stremio-git' 'stremio-legacy' 'stremio-beta')
source=("${_pkgname}::git+https://github.com/jimzrt/stremio-shell.git#branch=feature/downmix")
sha256sums=('SKIP')

pkgver() {
    cd "${srcdir}/${_pkgname}"
    git describe --long --tags --match 'v[0-9]*' | sed -E 's/^v//;s/([^-]+)-([0-9]+)-g/\1.r\2.g/;s/-/./g'
}

prepare() {
    cd "${srcdir}/${_pkgname}"
    git submodule update --init --recursive
}

build() {
    cd "${srcdir}/${_pkgname}"
    make -f release.makefile
}

package() {
    cd "${srcdir}/${_pkgname}"
    make -f release.makefile PREFIX="${pkgdir}" install
    sed 's/^Icon=.*/Icon=stremio-downmix/' smartcode-stremio.desktop \
        > "${pkgdir}/usr/share/applications/stremio-downmix.desktop"
    install -Dm644 images/stremio.svg \
        "${pkgdir}/usr/share/icons/hicolor/scalable/apps/stremio-downmix.svg"
}
