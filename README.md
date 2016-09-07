To build the OpenWrt snap you need a recent Linux distribution or Mac OS X
as long as gcc, make, awk, ncurses, openssl and zlib are installed.
On Ubuntu you can install everything with:
`apt install build-essential libncurses5-dev zlib1g-dev libssl-dev gawk`

Update the feeds package and install LUCI from the feeds
```
$ scripts/feeds update
Updating feed 'luci' from 'https://git.lede-project.org/project/luci.git' ...
Cloning into './feeds/luci'...
Create index file './feeds/luci.index'
$ scripts/feeds install luci
Installing package 'luci' from luci
Installing package 'luci-mod-admin-full' from luci
Installing package 'luci-base' from luci
Installing package 'luci-lib-nixio' from luci
Installing package 'luci-lib-ip' from luci
Installing package 'luci-lib-jsonc' from luci
Installing package 'luci-theme-bootstrap' from luci
Installing package 'luci-app-firewall' from luci
Installing package 'luci-proto-ppp' from luci
Installing package 'luci-proto-ipv6' from luci
```
Run `$ make menuconfig` and configure the system by selecting the target architecture,
WiFi daemon and support scripts and add the snap output format.
Also remove dropbear to avoid conflict with Ubuntu sshd
```
Target System (Broadcom BCM27xx)  --->
Subtarget (BCM2710 based boards)  --->
Target Images  --->
  [*] snap
LuCI  --->
  1. Collections  --->
    <*> luci
Network  --->
  <*> wpad-mini... IEEE 802.1x Authenticator/Supplicant (WPA-PSK only)
Kernel modules  --->
  Wireless Drivers  --->
    <*> kmod-brcmfmac............... Broadcom IEEE802.11n USB FullMAC WLAN driver
    [*]   Enable SDIO bus interface support
Base system  --->
  < > dropbear....... Small SSH2 client/server
```
