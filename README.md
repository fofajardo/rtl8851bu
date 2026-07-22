# Realtek RTL8851BU Wi-Fi Driver for Linux

This repository hosts a modified and updated version of the Realtek RTL8851BU Wi-Fi driver for Linux. It is primarily tested on Arch Linux with a [COMFAST CF-943AX](https://www.alibaba.com/product-detail/COMFAST-RTL8851BU-Wireless-BT-Adapter-Dongle_1601014889255.html), but users of other distributions are welcome to contribute and report their experiences.

## Features
- Supports **IEEE 802.11 b/g/n/ac/ax**
- Implements **WPA3-SAE R3** security
- **Soft AP mode**, **WiFi-Direct**, and **Miracast** support
- **WOWLAN** (Wake on Wireless LAN)
- **Bluetooth coexistence (BT-COEXIST)**
- Site survey scanning and manual connection
- **WPS** - PIN and PBC Methods

## Supported Platforms
- **Linux Kernel Versions:** 3.13 to 7.1
- **CPU Architectures:** x86, ARM, MIPS

## Installation
For Arch Linux and its derivatives, the [`rtl8851bu-dkms-git`](https://aur.archlinux.org/packages/rtl8851bu-dkms-git) package offers a convenient DKMS-based installation. Alternatively, users can manually build and install the kernel modules using `make clean && make && sudo make install`. For non-Arch Linux users wishing to use DKMS, the command is `sudo dkms install .`, and they should be aware that the module installation path might need to be specified based on their distribution's kernel module directory structure.

## Contributing
Contributions are welcome! If you're using a different Linux distribution or kernel version, feel free to test and submit patches to improve compatibility. Please open an issue or pull request with your findings and fixes.

## Known Issues
This driver operates in concurrent mode by default, which may result in duplicate network interfaces appearing. To prevent potential issues, such as the Wi-Fi adapter crashing, mark the `ap0` interface as unmanaged if you're using NetworkManager. If you're using a different networking service, refer to its documentation for instructions on reserving the interface as unmanaged.  

Assuming you are using NetworkManager, either create or edit the `/etc/NetworkManager/NetworkManager.conf` file and add the following:  

```
[keyfile]                                                                    
unmanaged-devices=interface-name:ap0
```

Additionally, the interface name may vary based on your system configuration. If [Predictable Network Interface Names](https://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames/) are enabled, you can run the following command to identify which of the two interfaces should be reserved as unmanaged or used exclusively as an access point.

```
[mudspring ~]\% sudo dmesg | grep ap0
[   17.187051] rtl8851bu 2-1:1.2 wlp0s11u1i2: renamed from ap0
```

## Acknowledgments
This project is based on Realtek's official driver release **v1.19.10-78-gfbe3fba11.20240422**.

## Disclaimer
This project is maintained by independent developers and is not affiliated with, endorsed by, or supported by Realtek Corporation. The maintainers are not employees of Realtek.

## License
This project is licensed under the GNU General Public License v2. See the full license text [here](https://github.com/fofajardo/rtl8851bu/blob/master/LICENSE).
