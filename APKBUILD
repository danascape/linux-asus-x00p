# Reference: <https://postmarketos.org/vendorkernel>
# Kernel config based on: arch/arm64/configs/(CHANGEME!)

pkgname=linux-asus-x00p
pkgver=4.9.337
pkgrel=0
pkgdesc="Asus Max M1 kernel fork"
arch="aarch64"
_carch="arm64"
_flavor="asus-x00p"
url="https://kernel.org"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native"
makedepends="
	bash
	bc
	bison
	devicepkg-dev
	flex
	openssl-dev
	perl
"

# Source
_repository="linux-asus-X00P-4.9"
_commit="ce81e17bf2454c176998fea4c1e7a41fa07a4c3b"
_config="config-$_flavor.$arch"
source="
	$pkgname-$_commit.tar.gz::https://github.com/danascape/$_repository/archive/$_commit.tar.gz
	$_config
	always-boot-to-initramfs.patch
"
builddir="$srcdir/$_repository-$_commit"
_outdir="out"

prepare() {
	default_prepare
	. downstreamkernel_prepare
}

build() {
	unset LDFLAGS
	make O="$_outdir" ARCH="$_carch" CC="${CC:-gcc}" \
		KBUILD_BUILD_VERSION="$((pkgrel + 1 ))-postmarketOS"
}

package() {
	downstreamkernel_package "$builddir" "$pkgdir" "$_carch" \
		"$_flavor" "$_outdir"
}

sha512sums="
9d75c496ee023409ba7546c49f7ff8cf2c18ad96075cc1f52c3602a860ee66ae407ecdb8888d045c551fcd323ded65b6031c02fb9c2ec89b2a0147f0399a2162  linux-asus-x00p-ce81e17bf2454c176998fea4c1e7a41fa07a4c3b.tar.gz
d40656a000fb84428dc583a799dfa00c44790ed1397836a3c29bd3b694735dbaf02f863af7ee64eb85bb7b58884cbc04d94d3f0ee305b4a3cfd796105eb4014d  config-asus-x00p.aarch64
8c10d536075009ef3fc636db50c706820751eebf8c581c06e16f2e68776b73e7c2369fcfc0c7bbb7f4be462df39fd82234efaacd7654de96367aaf117a98fd5a  always-boot-to-initramfs.patch
"
