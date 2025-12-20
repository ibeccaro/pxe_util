# GPARTED in a PXE server linux box TFTP subfolder


### Preparation
- download Gparted live zip file and unzip
- copy files to root subfolder
			```sudo cp live/{vmlinuz,initrd.img} /srv/tftp/gpartedXX```
- copy squashfs to www
```
			sudo cp live/filesystem/squashfs /var/www/html
```
```
			mv /var/www/html/filesystem.squashfs /var/www/html/gpXX.filesystem.squashfs
```
- add /srv/tftp/gpartedXX/pxelinux.cfg/default
```
			label GPartedXX
            MENU LABEL GParted XX Live
            kernel gpartedXX/vmlinuz
            append initrd=gpartedXX/initrd.img boot=live config components union=overlay username=user noswap noeject vga=788 fetch=http://192.168.5.100/gpXX.filesystem.squashfs
```
- if the GParted live version you are using is <= 0.22.0-1, then the config file is like:
```
    label GPartedXX
            MENU LABEL GParted XX Live
            kernel gparteXX/vmlinuz
            append initrd=gpartedXX/initrd.img boot=live config union=aufs noswap noprompt vga=788 fetch=http://192.168.5.100/gpXX.filesystem.squashfs
```            

__NOTES__
notice in the line wich appends initrd the http reference to the squash filesystem file, published in the apache2 root dir for download via http (not the less reliable for larger file TFTP)


### References

https://gparted.org/livepxe.phpx