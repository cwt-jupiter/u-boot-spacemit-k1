# Maintainer: Chaiwat Suttipongsakul <cwt@bashell.com>

pkgname=u-boot-spacemit-k1
pkgver=2.1
pkgrel=1
pkgdesc='Das U-Boot supports SpacemiT Key Stone series CPU'
_tag=k1-bl-v${pkgver}-release
_srcname=uboot-2022.10-$_tag
url="https://gitee.com/bianbu-linux/uboot-2022.10"
arch=(riscv64)
license=('GPL-2.0+')
makedepends=(gcc swig)
options=('!strip')
source=("${_srcname}.tar.gz::${url}/repository/archive/${_tag}.tar.gz"
        '01-config-btrfs.patch'
        '02-config-substrings.patch'
        '03-config-512-console-input.patch')

b2sums=('4231c678d4fda8f210a7fa63dca5e5c9e33efebdbe848170a9eabfa93b27e9f0b9328ee5ebc512fbc77404b6d33478c41679a531b8c06c68cff2440e71caf07a'
        'f3c9d91de82e99b56477550edd73e24a5d24ce264f54f010c30342e8561e554dd23176cf5d75d1ac4de1489e414155a64ee999564cdf7eed1c750392fb3e974e'
        '1dde984839e0f9be5c46d4c1736d47e3ea6009e59add4b0c50efc28ce0c439e8e91ab2efb9af15916ab04b1dfd074709fe9115b66772fed9aca34290abdf2fd0'
        '5597bfbe1e9ac91c7f6b9f18bea565f867598f9559bf3b9c73b0eeb30a74363fc55b94040a91803f13cd1bc901bbeea53bb3dbb65cd4458c405ea3bed830ef2f')


prepare() {
  cd $_srcname
  make -j $(nproc) k1_defconfig
  local src
  for src in $(ls ../*.patch); do
    echo "Applying patch $src..."
    patch -Np1 <"../$src"
  done
}

build() {
  cd $_srcname
  make -j $(nproc)
}

package() {
  cd $_srcname
  install -Dm644 FSBL.bin "$pkgdir/usr/share/$pkgname/FSBL.bin"
  install -Dm644 u-boot-env-default.bin "$pkgdir/usr/share/$pkgname/u-boot-env-default.bin"
  install -Dm644 u-boot.itb "$pkgdir/usr/share/$pkgname/u-boot.itb"
}

# vim:set ts=8 sts=2 sw=2 et:
