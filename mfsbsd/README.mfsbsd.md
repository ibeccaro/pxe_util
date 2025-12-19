# Patched Makefile and tools/packages.sample for mfsbsd
Modified files to patch

https://github.com/mmatuska/mfsbsd

to make it work correctly on FreeBSD 14.3 i386 to generate i386 mfsbsd

(preliminary, fs produced are still untested)

ver 0.00.03-12-19-25\
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
 
 ## Notes
 Legacy i386 machine do not need EFI bootloader and it is not present in the distribuition (14.3),
 so it has been removed from makefile and still the makefile must be invoked with NO_EFIBOOT option set\
 More, the tools/packages,sample file installs cpdup-freebsd package from older FreeBSD releases, now 
 replaced by cpdup package.
 Replace
 
 ```Makefile``` and ```tools/packages.sample```
 
 with provided files and build,
 
 ### Instructions for building
 same as original mfsbsd butt adding ```NO_EFIBOOT=yes``` option (adding ```WITHOUT_EFI=yes``` can also help)
 
- disc image
```
make BASE=/cdrom/usr/freebsd-dist NO_EFIBOOT=yes
make BASE=/cdrom/10.2-RELEASE NO_EFIBOOT=yes
make CUSTOM=1 BUILDWORLD=1 BUILDKERNEL=1 NO_EFIBOOT=yes
```
- bootable ISO file:
```
make iso BASE=/cdrom/usr/freebsd-dist NO_EFIBOOT=yes
make iso BASE=/cdrom/10.2-RELEASE NO_EFIBOOT=yes
make iso CUSTOM=1 BUILDWORLD=1 BUILDKERNEL=1 NO_EFIBOOT=yes
```
- .tar.gz file:
```
make tar BASE=/cdrom/usr/freebsd-dist NO_EFIBOOT=yes
make tar BASE=/cdrom/10.2-RELEASE NO_EFIBOOT=yes
make tar CUSTOM=1 BUILDWORLD=1 BUILDKERNEL=1 NO_EFIBOOT=yes
```
- roothack edition:
```
make iso CUSTOM=1 BUILDWORLD=1 BUILDKERNEL=1 ROOTHACK=1 NO_EFIBOOT=yes
```
- special edition (with FreeBSD distribution):
```
make iso BASE=/cdrom/11.0-RELEASE RELEASE=11.0-RELEASE ARCH=amd64 NO_EFIBOOT=yes
```
- GCE-compatible .tar.gz file:
``` 
make gce BASE=/cdrom/11.0-RELEASE WITHOUT_EFI=yes
make gce CUSTOM=1 BUILDWORLD=1 BUILDKERNEL=1 NO_EFIBOOT=yes
```