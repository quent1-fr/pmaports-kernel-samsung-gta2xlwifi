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
_commit="20938a12951ba63bcbd824ebf1a9c7318c3b68d6"
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
16fcec6a241841b849a5df67384b5b962fa3d25371f74117a6d3f0995d7d65cd715340f396e40ad9144ce239a6a7ec83d368569a1d980a3621064343b40f64ff  linux-samsung-gta2xlwifi-20938a12951ba63bcbd824ebf1a9c7318c3b68d6.tar.gz
3b74639b0f13803ead0c2bdda480ee527ed7f812280fe4ed14e793b5725c83625d0cd2a979172725856b3100bd6836e4187f6dc84fd2739c190c167af368c53e  config-samsung-gta2xlwifi.aarch64
"
