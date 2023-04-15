# armbian-TVE-THD-fixes
**Raspberry Pi Zero (LTS)** Armbian binaries with fixes:
1. TV output
2. H3 temperature readings

In the ZIP archive are updated kernel binaries.
Unzip fist (due to GitHub files size limitation, archive is split).

## Installation

`dpkg -i linux-image-current-sunxi_23.05.0-trunk--6.1.23-S543a-De8b2-Pc3d3-Ce146Hfe66-HK01ba-V014b-Bf77d_armhf.deb`

`dpkg -i linux-dtb-current-sunxi_23.05.0-trunk--6.1.23-S543a-De8b2-Pc3d3-Ce146Hfe66-HK01ba-V014b-Bf77d_armhf.deb`

More info for TV out adjustment you can find here:
https://github.com/armbian/build/issues/5047

## Difference
CPU temperature before FIX at logon after boot:
```
  ___  ____  _   _____
 / _ \|  _ \(_) |__  /___ _ __ ___
| | | | |_) | |   / // _ \ '__/ _ \
| |_| |  __/| |  / /|  __/ | | (_) |
 \___/|_|   |_| /____\___|_|  \___/


Welcome to Armbian 23.05.0-trunk Bullseye with Linux 6.1.23-sunxi

No end-user support: built from trunk

System load:   2%               Up time:       22 min
Memory usage:  13% of 490M      IP:            192.168.10.223
CPU temp:      21°C             Usage of /:    5% of 29G

Last login: Wed Apr 12 18:26:00 2023 from 192.168.10.66\
```

CPU temperature after FIX at logon after boot:
```
  ___  ____  _   _____
 / _ \|  _ \(_) |__  /___ _ __ ___
| | | | |_) | |   / // _ \ '__/ _ \
| |_| |  __/| |  / /|  __/ | | (_) |
 \___/|_|   |_| /____\___|_|  \___/

Welcome to Armbian 23.05.0-trunk Bullseye with Linux 6.1.23-sunxi

No end-user support: built from trunk

System load:   18%              Up time:       1 min
Memory usage:  13% of 490M      IP:            192.168.10.223
CPU temp:      31°C             Usage of /:    5% of 29G

Last login: Sat Apr 15 15:05:55 2023 from 192.168.10.66
```

## Long-term trend:

<img width="709" alt="OPi-Monitor - load,speed,temperature" src="https://user-images.githubusercontent.com/5048591/232230631-06a93377-7920-44de-b26c-e45e44ae470a.png">

Temperature is "low" even Opi Zero is in the Orange Pi black box with extension board inside.
CPU has only passive small heatsing.
* High peak at 15:09 was start of packages installations.
* Since 15:37 started compilnng of ffmpeg form sources.

## DEBUG
There is also activated DEBUG of h3 calibration value burned in chip.

Search `/var/log/system` for this string:

`Apr 15 15:09:13 orangepizero kernel: [    9.460261] sun8i-thermal 1c25000.thermal-sensor: DEBUG: h3 caldata=0x07ed=2029, callen=4`

In my case calibration value is **caldata=0x07ed=2029**
