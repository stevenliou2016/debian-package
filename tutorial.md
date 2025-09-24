# Make your own Debian package(.deb)

:::info
:bulb: Environment: Ubuntu 20.04.6 LTS, dpkg 1.19.7
:::

## What is Debian package?

The main purpose of a Debian package is to provide a consistent method for **installing, upgrading, configuring, and removing programs**.  

Packages are divided into two types: **source package (.dsc)** and **binary packages (.deb)**.  

**source package (.dsc)**: Primarily contains the source code.  
**binary package (.deb)**: Primarily contains executable files.  

This article will focus on introducing the **binary package**.

## Binary package

The example demonstrates packaging a program that displays "hello world!" in the terminal into a .deb file and creating an icon for the program on the desktop.  

Below is the structure of the hello-world packaging folder:
```
hello-world
├── DEBIAN
│   └── control
└── usr
    ├── bin
    │   └── hello-world
    └── share
        ├── applications
        │   └── hello-world.desktop
        └── icons
            └── hello-world.png
```
:::danger
Note: The DEBIAN/control file is mandatory; otherwise, dpkg-deb will report an error.
:::

### :small_blue_diamond: hello-world source code
```
#include<iostream>

int main(){
    std::cout << "hello world!" << std::endl;
    system("sleep 2");
    return 0;
}
```
:::info
Compilation command: g++ hello-world.cpp -o hello-world  
Place the executable hello-world in hello-world/usr/bin.
:::
### :small_blue_diamond: control file
```
Package: hello-world
Version: 1.0.0
Architecture: amd64
Maintainer: Your Name <your.email@example.com>
Installed-Size: 68
Section: Utility
Priority: optional
Description: This is a hello world example.
```
Package: Package name  
Version: Debian Package version  
:::info
Debian version numbers typically follow the format major.minor.patch
:::
Architecture: Specifies applicable architectures  
:::info
all: Suitable for all architectures, no rebuild required  
any: Can be built successfully on any architecture  
amd64: Suitable for 64-bit architectures (**x86_64**)  
:::
Maintainer: Maintainer information  
Installed-Size: Informs the user of the installed file size to estimate space, in **KB**  
Section: Package category  
:::info
**Utility** indicates a tool category  
:::
Priority: Package priority  
:::info
**optional** is the standard setting for most non-essential packages  
:::
Description: Package description  
```
The above information can be viewed with the command:

~$apt show hello-world
Package: hello-world
Version: 1.0.0
Status: install ok installed
Priority: optional
Section: Utility
Maintainer: Your Name <your.email@example.com>
Installed-Size: 69.6 kB
Download-Size: unknown
APT-Manual-Installed: yes
APT-Sources: /var/lib/dpkg/status
Description: This is a hello world example.
```
:::info
Place the control file in hello-world/DEBIAN
:::

### :small_blue_diamond: hello-world.desktop (optional)
```
[Desktop Entry]
Version=1.0
Name=hello-world
Comment=hello-world.
Exec='/usr/bin/hello-world'
Icon=hello-world.png
Terminal=true
Type=Application
Categories=Utility;Development;
```
Version= : Format version of the .desktop file  
Name= : Display name of the application  
Comment= : Description of the application  
Exec= : Command to launch the application  
Icon= : Application icon  
:::info
dpkg automatically searches for the icon in hello-world/usr/share/icons. If the icon is not in the standard path, specify the full path.  
:::
Terminal= : Whether to run in a terminal  
Type= : Specifies the type  
:::info
Options include Application, Link, or Directory.
:::
Categories= : Specifies the category
:::info
Place hello-world.desktop in hello-world/usr/share/applications/.
:::
          