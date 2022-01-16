# Reference: <https://postmarketos.org/vendorkernel>
# Kernel config based on: arch/arm64/configs/(CHANGEME!)

pkgname=linux-asus-x00p
pkgver=3.18.140
pkgrel=0
pkgdesc="ASUS Asus Max M1 kernel fork"
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
_repository="android_kernel_asus_msm8937"
_commit="d6a60bdad63f7b50edcd93ebc7790c1dab7ce09f"
_config="config-$_flavor.$arch"
source="
	$pkgname-$_commit.tar.gz::https://github.com/LineageOS/$_repository/archive/$_commit.tar.gz
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
09b02b3a2e4d99e717170ff4ef6d7fe2bf71bece23d2e5acccfb7a15a110f8c89f2b14ba6aab8f39482ab4e3e7929ef3c5a910107caa408d6ad3e8b7ca0196e7  linux-asus-x00p-d6a60bdad63f7b50edcd93ebc7790c1dab7ce09f.tar.gz
5163960433de3064bcaa1651fa73fb10848a6f04fdb09bcd57185cc24ba1cb8eaea5c417de7f0739a4be8b82c9b8479b2af903865c6d1cb6b39a335200a2352d  config-asus-x00p.aarch64
8c10d536075009ef3fc636db50c706820751eebf8c581c06e16f2e68776b73e7c2369fcfc0c7bbb7f4be462df39fd82234efaacd7654de96367aaf117a98fd5a  always-boot-to-initramfs.patch
"
