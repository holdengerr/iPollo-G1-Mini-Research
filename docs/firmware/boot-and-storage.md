# Boot and Storage

## Confirmed

- The host board uses **SPI NOR flash** for boot and root storage.
- Observed flash device: `EN25QH128A-104HIP`
- Capacity: **16 MB**
- Stock Linux exposes MTD partitions.

## Observed stock partition map

| Partition | Size | Notes |
| --- | ---: | --- |
| `u-boot` | `0x000c0000` | bootloader |
| `bootenv` | `0x00020000` | boot environment |
| `dtb` | `0x00020000` | device tree blob |
| `kernel` | `0x00300000` | Linux kernel |
| `rootfs` | `0x00bf0000` | root filesystem |
| `rootfs_data` | `0x00610000` | writable overlay/data |
| `otp` | `0x00010000` | one-time-programmable or reserved region |

## Inferred

- The stock boot flow appears to be conventional for a small OpenWrt-like SPI NOR system: bootloader -> DTB -> kernel -> squashfs rootfs plus writable data partition.

## Unknown

- Full vendor upgrade path details
- Exact stock flashing toolchain used by the vendor

## Evidence

- Live Linux inventory on stock-like boot exposed `/proc/mtd` with the partition names above.
