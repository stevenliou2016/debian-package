# debian-package

This is a hello world example. Refer to tutorail for detail.  

## Usage

Package folder hello-world in hello-world.deb
```
~$ dpkg -b hello-world/
dpkg-deb: building package 'hello-world' in 'hello-world.deb'.
```
Install package
```
~$ sudo dpkg -i hello-world.deb
```
Show information about package
```
~$ apt show hello-world 
Package: hello-world
Version: 1.0.0
Status: install ok installed
Priority: optional
Section: Utility
Maintainer: Your Name <your.email@example.com>
Installed-Size: 69.6 kB
Download-Size: 不明
APT-Manual-Installed: yes
APT-Sources: /var/lib/dpkg/status
Description: This is a hello world example.
```
Uninstall package
```
~$ sudo dpkg -r hello-world
```
