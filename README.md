# Prebuilt kernel and bootloader: Radxa ROCK 5

Prebuilt binaries for the open AOSP 15 port for the Radxa ROCK 5 family, checked out at
`device/radxa/rock5-kernel` by [android_local_manifest_rock5](https://github.com/RadicalES/android_local_manifest_rock5).
They are built with the scripts in [android_device_radxa_rock5](https://github.com/RadicalES/android_device_radxa_rock5).

| File | What | Built with |
|---|---|---|
| `Image` | Linux 6.18.63 (mainline LTS), arm64 | `kernel/build-kernel.sh` (AOSP clang) |
| `*.dtb` | RK3588/RK3588S ROCK 5 device trees, from the same kernel | same |
| `config` | the kernel's final `.config` | same |
| `version` | kernel version | same |
| `u-boot-rockchip.bin` | U-Boot v2026.10 (`rock5b-rk3588_defconfig`) + TF-A v2.15.0 BL31 + Rockchip DDR init blob | `bootloader/build-uboot.sh` |

`u-boot-rockchip.bin` is written at sector 64 of the boot medium (`tools/mkimg.sh` does this).

Each commit that updates a binary names the device-tree commit and versions it was built from.

## Sources and licences

- **Linux** (GPL-2.0): `linux-6.18.63.tar.xz` from kernel.org, configured as recorded in `config`
  (defconfig + AOSP `android-base.config` + the device tree's `kernel/rock5.config`). GPU and NIC firmware
  from linux-firmware is embedded (`mali_csffw.bin`, `rtl8125b-2.fw`) under its own licences.
- **U-Boot** (GPL-2.0+): tag `v2026.10` from source.denx.de/u-boot/u-boot, `rock5b-rk3588_defconfig`.
- **TF-A** (BSD-3-Clause): tag `v2.15.0` from github.com/ARM-software/arm-trusted-firmware, platform `rk3588`.
- **DDR init blob** (closed, Rockchip): `rk3588_ddr_lp4_2112MHz_lp5_2400MHz_v1.24.bin` from
  github.com/rockchip-linux/rkbin, redistributed under the rkbin licence.
