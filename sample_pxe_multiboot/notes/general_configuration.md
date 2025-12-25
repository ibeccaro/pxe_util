# GENERAL SETUP of PXE server on Debian


## DHCP

```
sudo apt install isc-dhcp-server,
```

example /etc/dhcp/dhcpd.conf

```
default-lease-time 600;
max-lease-time 7200;

allow booting;

# in this example, we serve DHCP requests from 192.168.0.(3 to 253)
# and we have a router at 192.168.0.1
subnet 192.168.0.0 netmask 255.255.255.0 {
  range 192.168.0.3 192.168.0.253;
  option broadcast-address 192.168.0.255;
  option routers 192.168.0.1;             # our router
  option domain-name-servers 192.168.0.1; # our router has DNS functionality
  next-server 192.168.0.2;                # our Server
  filename "pxelinux.0"; # setting a default, might be wrong for "non defaults"
}

group {
  next-server 192.168.0.2;                # our Server
  host tftpclient {
    # attempt to provide better match for architecture and bootfile
    if option architecture-type = 00:07 {
      filename "debian-installer/amd64/bootnetx64.efi";
    } else {
      filename "pxelinux.0";
    }
  }
}
```

```
sudo systemctl restart isc-dhcp-server
```

## TFTP

```
sudo apt install tftp
```

example /etc/default/tftpd-hpa

```
  TFTP_USERNAME="tftp"
  TFTP_DIRECTORY="/srv/tftp"
  TFTP_ADDRESS="0.0.0.0:69"
  TFTP_OPTIONS="--secure"
```

```
sudo systemctl restart tftpd-hpa
```

## WWW
some oses may require to transfer larfe fiiles, this can be done with NFS or HTTP

```
sudo apt install apache2
```

and the files referenced may be placed in /var/www/html


## PXELINUX/SYSLINUX

```
sudo apt install syslinux pxelinux
```

installs:\
	- pxelinux.0 (NBP)
	- BIOS (legacy machines) modules .c32
	- EFI modules
	
in the following locations

```
/usr/lib/PXELINUX/pxelinux.0
/usr/lib/syslinux/modules/bios/
/usr/lib/syslinux/modules/efi64/
```

- on RHEL
```
sudo dnf install syslinux syslinux-tftpboot
```

- on ARCH
```
sudo pacman -S syslinux
```

- minimum recomended modules
```
ldlinux.c32
menu.c32
libutil.c32
libcom32.c32
vesamenu.c32
pxechn.c32
```

## pxelinux.cfg/default

example
```
DEFAULT menu.c32
PROMPT 0
TIMEOUT 50

MENU TITLE PXE Boot Menu

LABEL local
    MENU LABEL Boot from local disk
    LOCALBOOT 0

LABEL memtest
    MENU LABEL Memtest86+
    KERNEL memtest
```

## PERMISSIONS

```
sudo chown -R tftp:tftp /srv/tftp
sudo chmod -R 755 /srv/tftp
```

## TROUBLESHOOTING
most errors on PXE client boot, in particular talking of not found files depends on
	- file path not corrext (NBP from the os expects often files in a specific structure)
	- owner (if the server can't access file the it's not found)
	- permissions (if files has not correct permissions, same as above, additionally the with --secure TFTP option often files with 777 perms are not reliable for transfer)
	
## ACTIVATING DAEMONS

```
sudo systemctl enable isc-dhcp-server
sudo systemctl enable tftpd

## EFI

pxelinux does not support EFI, for EFI use

```
syslinux.efi
ldlinux.e64
```
	