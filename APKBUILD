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

sha512sums="(run 'pmbootstrap checksum linux-asus-x00p' to fill)"
