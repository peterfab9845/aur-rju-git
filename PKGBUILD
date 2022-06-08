# Maintainer: peterfab9845 <archlinux@peterfab.com>
pkgname=rju-git
pkgver=r218.ab8212e
pkgrel=1
pkgdesc="Various jackd utilities"
arch=('x86_64')
url=""
license=('GPL')
groups=()
depends=('libsndfile' 'libsamplerate' 'liblo' 'jack2' 'libpng' 'libxext')
makedepends=('git' 'vst2sdk')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
replaces=()
backup=()
options=()
install=
source=('git+https://gitlab.com/rd--/rju.git'
        'git+https://gitlab.com/rd--/r-common'
        'rju-git-build.patch')
noextract=()
md5sums=('SKIP'
         'SKIP'
         'be9fa7eca8f20f8d6b2c4cd312c3defd')

pkgver() {
	cd "$srcdir/${pkgname%-git}"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
    cd "$srcdir/${pkgname%-git}"
    patch -p1 -i "$srcdir/${pkgname}-build.patch"
    git submodule init
    git config submodule.cmd/r-common.url "$srcdir/r-common"
    git submodule update
    sed -i '/xrealloc/d' cmd/r-common/c/file.h
}

build() {
	cd "$srcdir/${pkgname%-git}/cmd"
	make VST_SDK=/usr/include/vst36 all
}

package() {
	cd "$srcdir/${pkgname%-git}/cmd"
    mkdir -p "$pkgdir/usr/bin"
    mkdir -p "$pkgdir/usr/include"
	make prefix="$pkgdir/usr/" install
}
