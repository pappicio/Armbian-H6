how to install HomeAssistant Supervised on Allwinner H6 TvBoxes

repeate, only Android TVBOXES with Allwinner H6 CPU are comatible with this system!

ok let's go!

you can:

1) compile theese sources from original armbian githib

or 

2) download reasy2go system with Homeassistant Supervised installed.


1) you need:

an HDMI LCD and an USB keyboard to 1st time configure system;

balenaetcher tool to flash system into a microSD

use the system (arbian.img file compiled)

flash microSD with balenaetcher, choose the .img file, and flash it

connect the TVBOX to a LAN CABLE...

insert microSD into Allwinner H6 CPU TVBOX and power on it... 

confogure system, set passwor dfor root user and new user (I suggest pi name!)

into shell type:

sudo armbian-config, menu 2; manage wifi and choice your own wifi (SSID), insert password and connect to it 

winscp and putty to: configure all needed to install docjer and homeassistant supervised as next explained

open winscp, new connection and inser tvbox ip, usenrname and password, connect

now open shell, putty, (2 pc icon on top/left of winscp window)

type:

sudo apt update

sudo apt upgrade

from this link

https://github.com/home-assistant/supervised-installer


ans this one

https://github.com/home-assistant/os-agent/tree/main#using-home-assistant-supervised-on-debian

choice the .deb file for you archotecture (aarch64), so:

os-agent_1.3.0_linux_aarch64.deb

copy it using winscp into  /tmp folder of your tvbox (from tab on left to the tab on right selectin the tmp folder before copy)

so into shell type:

wget https://github.com/home-assistant/os-agent/releases/download/1.3.0/os-agent_1.3.0_linux_aarch64.deb

sudo dpkg -i os-agent_1.3.0_linux_aarch64.deb

continue to follow also this guide:

https://github.com/home-assistant/supervised-installer

and in graphic window choice the target system to instll HA: raspberry4-64bit (is good even debian system is.....)

wait for 20/30 minutes and finally, connect to:

http://ip-tvbox:8123




2)

download ready2go system from releases in thi github

and you need also:

an HDMI LCD and an USB keyboard to 1st time configure system;

balenaetcher tool to flash system into a microSD

use the system (arbian.img.gz image)

flash microSD with balenaetcher, choose the .img.gz system file, and flash it

connect the TVBOX to a LAN CABLE...

insert microSD into Allwinner H6 CPU TVBOX and power on it... 

into shell type:

sudo ifconfig so you can see the assigned IP.

now by winscp you can connect and have 2 user ready:

root (password: root)

pi   (passwor pi)

new connection on winscp, insert tvbox ip

usenrame:pi; password:pi

open remote shell 

and type:

sudo passwd root

(insert as asked pi password, so pi)

insert new root password twice, 

repeat:

sudo passwd pi

insert new pi password twice

ok, you now changed default root and pi password, write them somewhere ro remember if needed

if you have wrong feee psace on mivrosd, by shell write:

sudo bash /etc/init.d/resize2fs start

sudo reboot

now...

write on shell:

sudo armbian-config, 

menu 2; manage wifi and choice your own wifi (SSID), insert password and connect to it 

sudo reboot, wait 20/30 minutes and then you go to:

http://TVBOX-IP:8123 and enjoy

to configure homeassistant

in both 1 and 2, you can execute:

sudo armbian-config and menu 1, choice to write system into intenral emmc, voice nr:2, wait 5 minutes and then sgut down system, remove microsd

and power on tvbox


<>
<>
<>
<>
<>





























<p align="center">
  <a href="#build-framework">
  <img src=".github/armbian-logo.png" alt="Armbian logo" width="144">
  </a><br>
  <strong>Armbian Linux Build Framework</strong><br>
<br>
<a href=https://github.com/armbian/build/actions/workflows/build-train.yml><img alt="GitHub Workflow Status" src="https://img.shields.io/github/workflow/status/armbian/build/Build%20train?logo=githubactions&label=Kernel%20compile&logoColor=white&style=for-the-badge"></a>
<a href=https://github.com/armbian/build/actions/workflows/build-all-desktops.yml><img alt="GitHub Workflow Status" src="https://img.shields.io/github/workflow/status/armbian/build/Build%20All%20Desktops?logo=githubactions&logoColor=white&label=Images%20assembly&style=for-the-badge"></a>
<a href=https://github.com/armbian/build/actions/workflows/smoke-tests.yml><img alt="GitHub Workflow Status" src="https://img.shields.io/github/workflow/status/armbian/build/Smoke%20tests%20on%20DUTs?logo=speedtest&label=Smoke%20test&style=for-the-badge"></a>
 <br>

<br>
<a href=https://twitter.com/armbian><img alt="Twitter Follow" src="https://img.shields.io/twitter/follow/armbian?logo=twitter&style=flat-square"></a>
<a href=http://discord.armbian.com/><img alt="Discord" src="https://img.shields.io/discord/854735915313659944?label=Discord&logo=discord&style=flat-square"></a>
<a href=https://liberapay.com/armbian><img alt="Liberapay patrons" src="https://img.shields.io/liberapay/patrons/armbian?logo=liberapay&style=flat-square"></a>
</p>



## Table of contents

- [What this project does?](#what-this-project-does)
- [Getting started](#getting-started)
- [Compare with industry standards](#compare-with-industry-standards)
- [Download prebuilt images](#download-prebuilt-images)
- [Project structure](#project-structure)
- [Contribution](#contribution)
- [Support](#support)
- [Contact](#contact)
- [Contributors](#contributors)
- [Sponsors](#sponsors)
- [License](#license)

## What this project does?

- Builds custom kernel, image or a distribution optimized for low resource HW such as single board computers,
- Include filesystem generation, low-level control software, kernel image and bootloader compilation,
- Provides a consistent user experience by keeping system standards across different platforms.

## Getting started

### Basic requirements

- x64 or aarch64 machine with at least 2GB of memory and ~35GB of disk space for a virtual machine, container or bare metal installation,
- Ubuntu Jammy 22.04 x64 or aarch64 for native building or any [Docker](https://docs.armbian.com/Developer-Guide_Building-with-Docker/) capable x64 / aarch64 Linux for containerised,
- Superuser rights (configured sudo or root access).

### Simply start with the build script

```bash
apt-get -y install git
git clone https://github.com/armbian/build
cd build
./compile.sh
```

<a href="#how-to-build-an-image-or-a-kernel"><img src=".github/README.gif" alt="Armbian logo" width="100%"></a>

- Interactive graphical interface.
- The workspace will be prepared by installing the necessary dependencies and sources.
- It guides the entire process until a kernel package or ready-to-use image of the SD card is created.

### Build parameter examples

Show work in progress areas in interactive mode:

```bash
./compile.sh EXPERT="yes"
```

Run build framework inside Docker container:

```bash
./compile.sh docker
```

Build minimal CLI Armbian Focal image for Orangepi Zero. Use modern kernel and write image to the SD card:

```bash
./compile.sh \
BOARD=orangepizero \
BRANCH=current \
RELEASE=focal \
BUILD_MINIMAL=yes \
BUILD_DESKTOP=no \
KERNEL_ONLY=no \
KERNEL_CONFIGURE=no \
CARD_DEVICE="/dev/sda"
```

More information:

- [Building Armbian](https://docs.armbian.com/Developer-Guide_Build-Preparation/) — how to start, how to automate;
- [Build options](https://docs.armbian.com/Developer-Guide_Build-Options/) — all build options;
- [Building with Docker](https://docs.armbian.com/Developer-Guide_Building-with-Docker/) — how to build inside container;
- [User configuration](https://docs.armbian.com/Developer-Guide_User-Configurations/) — how to add packages, patches and override sources config;


## Download prebuilt images

- quarterly released **supported** builds —  <https://www.armbian.com/download>
- weekly released **unsupported** community builds —  <https://github.com/armbian/community>
- upon code change **unsupported** development builds —  <https://github.com/armbian/build/releases>

## Compare with industry standards

Check similarity, advantages and disadvantages compared with leading industry standard build software.

Function | Armbian | Yocto | Buildroot |
|:--|:--|:--|:--|
| Target | general purpose | embedded | embedded / IOT |
| U-boot and kernel | compiled from sources | compiled from sources | compiled from sources |
| Board support maintenance &nbsp; | complete | outside | outside |
| Root file system | Debian or Ubuntu based| custom | custom |
| Package manager | APT | any | none |
| Configurability | limited | large | large |
| Initramfs support | yes | yes | yes |
| Getting started | quick | very slow | slow |
| Cross compilation | yes | yes | yes |

## Project structure

```text
├── cache                                Work / cache directory
│   ├── rootfs                           Compressed userspace packages cache
│   ├── sources                          Kernel, u-boot and various drivers sources.
│   ├── toolchains                       External cross compilers from Linaro™ or ARM™
├── config                               Packages repository configurations
│   ├── targets.conf                     Board build target configuration
│   ├── boards                           Board configurations
│   ├── bootenv                          Initial boot loaders environments per family
│   ├── bootscripts                      Initial Boot loaders scripts per family
│   ├── cli                              CLI packages configurations per distribution
│   ├── desktop                          Desktop packages configurations per distribution
│   ├── distributions                    Distributions settings
│   ├── kernel                           Kernel build configurations per family
│   ├── sources                          Kernel and u-boot sources locations and scripts
│   ├── templates                        User configuration templates which populate userpatches
│   └── torrents                         External compiler and rootfs cache torrents
├── extensions                           extend build system with specific functionality
├── lib                                  Main build framework libraries
├── output                               Build artifact
│   └── deb                              Deb packages
│   └── images                           Bootable images - RAW or compressed
│   └── debug                            Patch and build logs
│   └── config                           Kernel configuration export location
│   └── patch                            Created patches location
├── packages                             Support scripts, binary blobs, packages
│   ├── blobs                            Wallpapers, various configs, closed source bootloaders
│   ├── bsp-cli                          Automatically added to armbian-bsp-cli package 
│   ├── bsp-desktop                      Automatically added to armbian-bsp-desktopo package
│   ├── bsp                              Scripts and configs overlay for rootfs
│   └── extras-buildpkgs                 Optional compilation and packaging engine
├── patch                                Collection of patches
│   ├── atf                              ARM trusted firmware
│   ├── kernel                           Linux kernel patches
|   |   └── family-branch                Per kernel family and branch
│   ├── misc                             Linux kernel packaging patches
│   └── u-boot                           Universal boot loader patches
|       ├── u-boot-board                 For specific board
|       └── u-boot-family                For entire kernel family
├── tools                                Tools for dealing with kernel patches and configs
└── userpatches                          User: configuration patching area
    ├── lib.config                       User: framework common config/override file
    ├── config-default.conf              User: default user config file
    ├── customize-image.sh               User: script will execute just before closing the image
    ├── atf                              User: ARM trusted firmware
    ├── kernel                           User: Linux kernel per kernel family
    ├── misc                             User: various
    └── u-boot                           User: universal boot loader patches
```

## 🙌 Contribution

### You don't need to be a programmer to help! 
- The easiest way to help is by "Starring" our repository - it helps more people find our code.
- [Check out our list of volunteer positions](https://forum.armbian.com/staffapplications/) and choose what you want to do ❤️
- [Seed torrents](https://forum.armbian.com/topic/4198-seed-our-torrents/)
- Help with [forum moderating](https://forum.armbian.com/topic/12631-help-on-forum-moderating/)
- [Project administration](https://forum.armbian.com/forum/39-armbian-project-administration/)
- [Donate](https://www.armbian.com/donate).

### Want to become a maintainer?

Please review the [Board Maintainers Procedures and Guidelines](https://docs.armbian.com/Board_Maintainers_Procedures_and_Guidelines/) and if you can meet the requirements as well as find a board on the [Board Maintainers](https://docs.armbian.com/Release_Board-Maintainers/) list which has less than 2 maintainers, then please apply using the linked form.

### Want to become a developer?

If you want to help with development, you should first review the [Development Code Review Procedures and Guidelines](https://docs.armbian.com/Development-Code_Review_Procedures_and_Guidelines/) and then you can review the pre-made Jira dashboards and additional resources provided below to find open tasks and how you can assist:

- [pull requests that needs a review](https://github.com/armbian/build/pulls?q=is%3Apr+is%3Aopen+review%3Arequired)
- dashboard for [junior](https://armbian.atlassian.net/jira/dashboards/10000) and [seniors](https://armbian.atlassian.net/jira/dashboards/10103) developers
- [documentation](https://docs.armbian.com/)
- [continuous integration](https://docs.armbian.com/Process_CI/)

## Support

Armbian is free software and provides **best effort help** through [community forums](https://forum.armbian.com/). Make sure to use help of [general project search engine](https://www.armbian.com/search) and [documentation](https://docs.armbian.com) before opening new forum topic. In case you require attention, buy appropriate [subscription level](https://forum.armbian.com/subscriptions) before asking for dedicated attention to the issue you have https://www.armbian.com/contact.

## Contact

- [Forums](https://forum.armbian.com) for Participate in Armbian
- IRC: `#armbian` on Libera.chat
- Discord: [http://discord.armbian.com](http://discord.armbian.com)
- Follow [@armbian](https://twitter.com/armbian) on Twitter or [LinkedIn](https://www.linkedin.com/company/armbian).
- Bugs: [issues](https://github.com/armbian/build/issues) / [JIRA](https://armbian.atlassian.net/jira/dashboards/10000)

## Contributors

Thank you to all the people who already contributed Armbian!

<a href="https://github.com/armbian/build/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=armbian/build" />
</a>

### Also

- [Current and past contributors](https://github.com/armbian/build/graphs/contributors), our families and friends.
- [Support staff](https://forum.armbian.com/members/2-moderators/) that keeps forums usable.
- [Individuals](https://forum.armbian.com/) that help with their ideas, reports and [donations](https://www.armbian.com/donate).

## Sponsors

Most of the project is sponsored with a work done by volunteer collaborators, while some part of the project costs are being covered by the industry. We would not be able to get this far without their help.

[Would you like your name to appear below?](https://www.armbian.com/#contact)

<a href="https://www.armbian.com/download/?tx_maker=xunlong" target="_blank"><img border=0 src="https://www.armbian.com/wp-content/uploads/2018/03/orangepi-logo-150x150.png" width="122" height="122"></a><a href="https://www.armbian.com/download/?tx_maker=friendlyelec" target="_blank"><img border=0 src="https://www.armbian.com/wp-content/uploads/2018/02/friendlyelec-logo-150x150.png" width="122" height="122"></a><a href="https://k-space.ee" target="_blank"><img border=0 src="https://www.armbian.com/wp-content/uploads/2018/03/kspace-150x150.png" width="122" height="122"></a><a href="https://www.innoscale.net" target="_blank"><img border=0 src="https://www.armbian.com/wp-content/uploads/2020/07/innoscale-2-150x150.png" width="122" height="122"></a><a href="https://www.armbian.com/download/?tx_maker=olimex" target="_blank"><img border=0 src="https://www.armbian.com/wp-content/uploads/2018/02/olimex-logo-150x150.png" width="122" height="122"></a><a href="https://www.armbian.com/download/?tx_maker=kobol" target="_blank"><img border=0 src="https://www.armbian.com/wp-content/uploads/2020/06/Kobol_logo-150x150.png" width="122" height="122"></a><a href="https://github.com/WorksOnArm/cluster/issues/223" target="_blank"><img border=0 src="https://www.armbian.com/wp-content/uploads/2020/11/work-on-arm-150x150.png" width="122" height="122"></a><a href="https://fosshost.org/" target="_blank"><img border=0 src="https://www.armbian.com/wp-content/uploads/2020/11/foss-host-150x150.png" width="122" height="122"></a><a href="https://nlnet.nl/" target="_blank"><img border=0 src="https://www.armbian.com/wp-content/uploads/2022/01/nlnet-fundation-150x150.png" width="122" height="122"></a><a href="#"><img border=0 src="https://www.armbian.com/wp-content/uploads/2021/06/lanecloud-150x150.png" width="122" height="122"></a><a href="https://www.khadas.com/" target="_blank"><img border=0 src="https://www.armbian.com/wp-content/uploads/2021/05/khadas-150x150.png" width="122" height="122"></a>

## License

This software is published under the GPL-2.0 License license.
