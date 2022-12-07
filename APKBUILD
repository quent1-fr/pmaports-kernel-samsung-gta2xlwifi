# Kernel config based on: postmarketos-qcom-msm8953

_flavor="samsung-gta2xlwifi"
pkgname=linux-$_flavor
pkgver=5.18.3
pkgrel=2
pkgdesc="Samsung Galaxy Tab A 10.5 2018 kernel, based on Mainline kernel fork for Qualcomm MSM8953 devices"
arch="aarch64"
url="https://github.com/quent1-fr/msm8953-mainline-linux"
license="GPL-2.0-only"
options="!strip !check !tracedeps
	pmb:cross-native
	pmb:kconfigcheck-waydroid
	pmb:kconfigcheck-nftables
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

_carch="arm64"
# Source
_commit="458e9e267d6638936df59b53aaff47a4dff0d2b4"
source="
	$pkgname-$_commit.tar.gz::https://github.com/quent1-fr/msm8953-mainline-linux/archive/$_commit.tar.gz
	config-$_flavor.$arch
"
builddir="$srcdir/linux-$_commit"

prepare() {
	default_prepare
	
	mkdir -p "$builddir"
	tar xvzf $pkgname-$_commit.tar.gz -C "$builddir" --strip 1
        cp "$srcdir/config-$_flavor.$arch" "$builddir/.config"
}

build() {
	unset LDFLAGS
	make ARCH="$_carch" CC="${CC:-gcc}" \
		KBUILD_BUILD_VERSION=$((pkgrel + 1 ))
}

package() {
	mkdir -p "$pkgdir"/boot
	make zinstall modules_install dtbs_install \
		ARCH="$_carch" \
		INSTALL_MOD_STRIP=1 \
		INSTALL_PATH="$pkgdir"/boot \
		INSTALL_MOD_PATH="$pkgdir" \
		INSTALL_DTBS_PATH="$pkgdir"/usr/share/dtb

	install -D "$builddir"/include/config/kernel.release \
		"$pkgdir"/usr/share/kernel/$_flavor/kernel.release

}
sha512sums="
ef1f82c9ff1f16bd4da7b01ee4b793df1b7e241792f15241bf16db3000457e140ccf423f9fc375f2f250a0e5113df1b153c3b5276892fc957602e32ce184ff25  linux-samsung-gta2xlwifi-458e9e267d6638936df59b53aaff47a4dff0d2b4.tar.gz
296c115b284a2d43eb16986be8ae5b32146a86667e48370a5e4e05444602063a3e287d799b2f60d9b237319d4371939fcb16652b36c23db43700d2946f22d314  config-samsung-gta2xlwifi.aarch64
"
