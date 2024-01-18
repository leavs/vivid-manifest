Vivid Repo Manifest README
==========================

This repo is used to download manifests for Vivid SDK releases.

Specific instructions will reside in READMEs in each branch.

Set up an Development Environment
---------------------------------

It is recommended to use Ubuntu 20.04 for compilation. Other Linux versions may need to adjust the software package accordingly. In addition to the system requirements, there are other hardware and software requirements.

Hardware requirements: 64-bit system, hard disk space should be greater than 40G. If you do multiple builds, you will need more hard drive space.

Software requirements: Ubuntu 20.04 system:
Please install software packages with below commands to setup SDK compiling environment:

```
$: sudo apt-get update
$: sudo apt-get install git ssh make gcc libssl-dev liblz4-tool expect \
g++ patchelf chrpath gawk texinfo chrpath diffstat binfmt-support \
qemu-user-static live-build bison flex fakeroot cmake gcc-multilib \
g++-multilib unzip device-tree-compiler ncurses-dev libgucharmap-2-90-dev \
bzip2 expat gpgv2 cpp-aarch64-linux-gnu time mtd-utils python3-pip zstd curl \
python-is-python3
$: sudo pip3 install asciidoc
```

It is recommended to use Ubuntu 20.04 system or higher version for development. If you encounter an error during compilation, you can check the error message and install the corresponding software packages accordingly.

Set up git
----------

Set up your email and name if you didn't set it before for git.
Replace the following "you@example.com" and "Your Name" to yours.

```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```


Install the `repo` utility:
---------------------------

To use this manifest repo, the `repo` tool must be installed first.

```
$: mkdir ~/bin
$: curl http://commondatastorage.googleapis.com/git-repo-downloads/repo  > ~/bin/repo
$: chmod a+x ~/bin/repo
$: PATH=${PATH}:~/bin
```

Download the Debian Project SDK
-------------------------------

```
$: mkdir vivid-bsp-release
$: cd vivid-bsp-release
$: repo init -u https://github.com/leavs/vivid-manifest -b <branch name> [ -m <release manifest>]
$: repo sync
```

Each branch will have detailed READMEs describing exact syntax.

Examples
--------

To download the 5.10.110-1.0.0 release

```
$: cd vivid-bsp-release
$: repo init -u https://github.com/leavs/vivid-manifest -b vivid-linux-bullseye -m vivid-rk3399-5.10.110-1.0.0.xml
$: repo sync
```

Download the Debian prebuilt rootfs image
-----------------------------------------

The rootfs image will be released separatly. You can issue the following commands to add it to the SDK.

```
$: cd vivid-bsp-release
$: mkdir debian 
$: cd debian
$: wget -c https://www.vividunit.com/download/rootfs/rootfs-vivid-latest.img.xz
$: xz -d rootfs-vivid-latest.img.xz
$: ln -sf rootfs-vivid-latest.img.xz linaro-rootfs.img
```

Build an image:
---------------

```
$: cd vivid-bsp-release
$: ./build.sh BoardConfig-rk3399-vivid-unit-v13.mk
$: ./build.sh all
```

After done, you can get `prebuilt-rk3399-vivid-unit-v13-yyymmdd.img` from vivid-bsp-release/rockdev/ directory.


