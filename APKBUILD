# Reference: <https://postmarketos.org/vendorkernel>
# Kernel config based on: arch/arm/configs/(CHANGEME!)

pkgname=linux-samsung-gta2xlwifi
pkgver=3.18.140
pkgrel=0
pkgdesc="Samsung Galaxy Tab A 10.5 2018 kernel fork"
arch="aarch64"
_carch="arm64"
_flavor="samsung-gta2xlwifi"
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
	gcc6
"

# Compiler: GCC 6 (doesn't boot when compiled with newer versions)
if [ "${CC:0:5}" != "gcc6-" ]; then
	CC="gcc6-$CC"
	HOSTCC="gcc6-gcc"
	CROSS_COMPILE="gcc6-$CROSS_COMPILE"
fi

# Source
_repository="android_kernel_samsung_gta2xlwifi"
_commit="788d1aa959d402941e0dd501c3a37a8f85ae66a9"
_config="config-$_flavor.$arch"
source="
	$pkgname-$_commit.tar.gz::https://github.com/quent1-fr/$_repository/archive/$_commit.tar.gz
	$_config
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
b0bd7025aac1e14fcd55a1c4f84aff0524dd96610b4aea49ba43e602fc1c7c3d1cc31fe2ed2fec3708b6622d7b9f76c0626d955f08df52105abe77cc09122640  linux-samsung-gta2xlwifi-788d1aa959d402941e0dd501c3a37a8f85ae66a9.tar.gz
1234e2f877debd22c3939948c54fa7e56bdb56ff4324cfb70093bf7b07275a0e5da935983d16b5f992ea4e62f87da329ef86f637c533e70384973920b712cc0c  config-samsung-gta2xlwifi.aarch64
"
