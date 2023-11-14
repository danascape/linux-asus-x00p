# Reference: <https://postmarketos.org/vendorkernel>
# Kernel config based on: arch/arm64/configs/(CHANGEME!)

pkgname=linux-asus-x00p
pkgver=4.9.337
pkgrel=0
pkgdesc="Asus Max M1 kernel fork"
arch="aarch64"
_carch="arm64"
_flavor="asus-x00p"
url="https://github.com/MrArtemSid/linux-msm89x7"
license="GPL-2.0-only"
options="!strip !check !tracedeps
	pmb:cross-native
	pmb:kconfigcheck-community
"
makedepends="
	bash
	bc
	bison
	devicepkg-dev
	findutils
	flex
	openssl-dev
	perl
	postmarketos-installkernel
"

# Source
_repository="linux-msm89x7"
_commit="2ad34a0d01f23c55930394522af696b1cf26dc14"
_config="config-$_flavor.$arch"
source="
	$pkgname-$_commit.tar.gz::https://github.com/MrArtemSid/$_repository/archive/$_commit.tar.gz
	$_config
"
builddir="$srcdir/$_repository-$_commit"
_outdir="out"

prepare() {
	default_prepare
	cp "$srcdir/config-$_flavor.$arch" .config
}

build() {
	unset LDFLAGS
	make O="$_outdir" ARCH="$_carch" CC="${CC:-gcc}" \
		KBUILD_BUILD_VERSION="$((pkgrel + 1 ))-postmarketOS"
}

package() {
	mkdir -p "$pkgdir"/boot

	make zinstall modules_install dtbs_install \
		ARCH="$_carch" \
		INSTALL_PATH="$pkgdir"/boot \
		INSTALL_MOD_PATH="$pkgdir" \
		INSTALL_MOD_STRIP=1 \
		INSTALL_DTBS_PATH="$pkgdir/boot/dtbs"
	rm -f "$pkgdir"/lib/modules/*/build "$pkgdir"/lib/modules/*/source

	install -Dm644 "$builddir/include/config/kernel.release" \
		"$pkgdir/usr/share/kernel/$_flavor/kernel.release"
}


sha512sums="
982c57911cb1eb9c8d3acd1270216f45c916e009284bc7da327e7f8e6495d8b2bacb18f14773289dc2eab11d6e0ab44d4917fa059651155a90afcb06de1c8993  linux-asus-x00p-2ad34a0d01f23c55930394522af696b1cf26dc14.tar.gz
5f28c4866bf1c198e65a78b6aeea1fb9b5c2ec3f4af2e618a9df1e070c1fed034a5bf0fa3e8ffe3fe3ff086490cf407541863295f95476f99878d351ce8cf0f8  config-asus-x00p.aarch64
"
