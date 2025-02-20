# recipes

A set of [debos](https://github.com/go-debos/debos) recipes for building a
Debian-based image for the Asus Zenfone 3 (ZE520KL/ZE552KL).

The default user is `mobian` with password `1234`.

## Build

To build the image, you need to have `debos` and `bmaptool`. On a Debian-based
system, install these dependencies by typing the following command in a terminal:

```
sudo apt install debos bmap-tools xz-utils
```

If you want to build an image for a Qualcomm-based device, additional packages
are required, which you can install with the following command:

```
sudo apt install android-sdk-libsparse-utils yq mkbootimg
```

Building with disk encryption support will also require the package `cryptsetup` to be installed
on your host.

Do note that we recommend using Debian 13 (Trixie) as previous versions didn't
include the `yq` package.

Similarly, if you want to use F2FS for the root filesystem (which isn't such a
good idea, as it has been known to cause corruption in the past), you'll need to
install `f2fs-tools` as well.

The build system will cache and re-use it's output files. To create a fresh build
remove `*.tar.gz`, `*.sqfs` and `*.img` before starting the build.

If your system isn't debian-based (or if you choose to install `debos` without
using `apt`, which is a terrible idea), please make sure you also install the
following required packages:
- `debootstrap`
- `qemu-system-x86`
- `qemu-user-static`
- `binfmt-support`

Then simply browse to the `mobian-recipes` folder and execute `./build.sh -t qcom-wip`.

You can use `./build.sh -d -t qcom-wip` to use the docker version of `debos`.

## Install

> TODO: Write lk2nd-specific install steps

Insert a MicroSD card into your computer, and type the following command:

```
sudo bmaptool copy <image> /dev/<sdcard>
```

or:

```
sudo dd if=<image> of=/dev/<sdcard> bs=1M
```

*Note: Make sure to use your actual SD card device, such as `mmcblk0` instead of
`<sdcard>`.*

**CAUTION: This will format the SD card and erase all its contents!!!**

## Contributing

If you want to help with this project, please have a look at the
[roadmap](https://wiki.debian.org/Teams/Mobian/Roadmap) and
[open issues](https://salsa.debian.org/Mobian-team/mobian-recipes/-/issues).

In case you need more information, feel free to get in touch with the developers
on [#mobian:matrix.org](https://matrix.to/#/#mobian:matrix.org)

# License

This software is licensed under the terms of the GNU General Public License,
version 3.
