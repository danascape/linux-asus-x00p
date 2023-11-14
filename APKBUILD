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
_commit="bf4d45fa42795e58f133113bdfb7de8c85656039"
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
7133766494551d14585c0d87db95b3c78b9c74f6bd4d72d85d7cbffcd328b14fb5e01c4dbf234aea887ebc8bb23f84bba72f28b1d68b396bb38047feb42da7e7  linux-asus-x00p-bf4d45fa42795e58f133113bdfb7de8c85656039.tar.gz
6f72f5e51e88ffef3b74d4898a19bae2233e4940cd163d8ae916b3f0ad45cf42897b55e6b9ff0b24412526ae5dda7f040508281df42da6d751a091de924d8ef6  config-asus-x00p.aarch64
8c10d536075009ef3fc636db50c706820751eebf8c581c06e16f2e68776b73e7c2369fcfc0c7bbb7f4be462df39fd82234efaacd7654de96367aaf117a98fd5a  always-boot-to-initramfs.patch
"
