# Sample PXE multiboot configuration
this folder contains a sample multiboot pxe server configuration on a linux box using pxelinux and syslinux

### Software used
 the software used in this implementation are:

- pxelinux
- syslinux
- isc-dhcp-server
- tftpd
- apache2

### Directories
it is assumed that the root TFTP folder is located at

- /srv/tftp
	- /srv/tftp/gpartedXX

and the web folder is located at

- /var/www/html

### Addresses

- The PXE server linux box is assumed to be: 192.168.5.100
- The subnet mask 255.255.255.0
- The gateway is assumed to be: 192.168.5.1

### Installation

### Configuration


ver 0.00.02-12-19-25 (preliminary)\
by
```   ____      ____..--'   ____      ____..--'    .-''-.    .---.     
 .'  __ `.  |        | .'  __ `.  |        |  .'_ _   \   | ,_|     
/   '  \  \ |   .-'  '/   '  \  \ |   .-'  ' / ( ` )   ',-./  )     
|___|  /  | |.-'.'   /|___|  /  | |.-'.'   /. (_ o _)  |\  '_ '`)   
   _.-`   |    /   _/    _.-`   |    /   _/ |  (_,_)___| > (_)  )   
.'   _    |  .'._( )_ .'   _    |  .'._( )_ '  \   .---.(  .  .-'   
|  _( )_  |.'  (_'o._)|  _( )_  |.'  (_'o._) \  `-'    / `-'`-'|___ 
\ (_ o _) /|    (_,_)|\ (_ o _) /|    (_,_)|  \       /   |        \
 '.(_,_).' |_________| '.(_,_).' |_________|   `'-..-'    `--------````
 ```
 