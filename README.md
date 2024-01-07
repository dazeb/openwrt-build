## This description has been translated and updated for Ubuntu 22.04.  

The original description is in Chinese and is located here https://github.com/Lienol/openwrt  

Sure, let's incorporate the new information into the process. Here's the updated process:

1. **Update your Ubuntu system**: Ensure your Ubuntu system is updated by running the following command:

```bash
sudo apt update
```

2. **Install necessary packages**: Install the necessary packages. Note that Python 2.7 is no longer needed as Python 3 is installed by default in Ubuntu 22.04. Here's the updated list of commands:

```bash
sudo apt install build-essential clang flex bison g++ gawk gcc-multilib g++-multilib gettext git libncurses-dev libssl-dev python3-distutils rsync unzip zlib1g-dev file wget
```

3. **Clone the OpenWRT repository**: Clone the OpenWRT repository. As of the time of writing, the latest version is 22.03, so we'll use that:

```bash
git clone -b 22.03 --single-branch https://github.com/Lienol/openwrt openwrt
cd openwrt
```

4. **Prepare the feeds**: Prepare the feeds. These are the package repositories that OpenWRT uses to fetch its software components:

```bash
./scripts/feeds clean
./scripts/feeds update -a
./scripts/feeds install -a
```

5. **Configure the build**: Run `make menuconfig` to configure your build. This will allow you to choose the target system, the toolchain, and the firmware packages you want to include.

6. **Download dependencies**: Before you can start the build, you need to download the dependencies. This can take a while depending on your internet connection:

```bash
make -j8 download V=s
```

7. **Start the build**: Finally, start the build. It's recommended to start with a single thread (`-j1`) for the first compilation to avoid potential issues:

```bash
make -j1 V=s
```

After the build completes, the output will be located in the `openwrt/bin/targets` directory.

Remember, this is a general guide and your specific needs might require additional steps or modifications. Always refer to the official OpenWRT documentation for the most accurate and up-to-date information.

![OpenWrt logo](include/logo.png)

OpenWrt Project is a Linux operating system targeting embedded devices. Instead
of trying to create a single, static firmware, OpenWrt provides a fully
writable filesystem with package management. This frees you from the
application selection and configuration provided by the vendor and allows you
to customize the device through the use of packages to suit any application.
For developers, OpenWrt is the framework to build an application without having
to build a complete firmware around it; for users this means the ability for
full customization, to use the device in ways never envisioned.

Sunshine!

## Development

To build your own firmware you need a GNU/Linux, BSD or MacOSX system (case
sensitive filesystem required). Cygwin is unsupported because of the lack of a
case sensitive file system.

### Requirements

You need the following tools to compile OpenWrt, the package names vary between
distributions. A complete list with distribution specific packages is found in
the [Build System Setup](https://openwrt.org/docs/guide-developer/build-system/install-buildsystem)
documentation.

```
binutils bzip2 diff find flex gawk gcc-6+ getopt grep install libc-dev libz-dev
make4.1+ perl python3.6+ rsync subversion unzip which
```

### Quickstart

1. Run `./scripts/feeds update -a` to obtain all the latest package definitions
   defined in feeds.conf / feeds.conf.default

2. Run `./scripts/feeds install -a` to install symlinks for all obtained
   packages into package/feeds/

3. Run `make menuconfig` to select your preferred configuration for the
   toolchain, target system & firmware packages.

4. Run `make` to build your firmware. This will download all sources, build the
   cross-compile toolchain and then cross-compile the GNU/Linux kernel & all chosen
   applications for your target system.

### Related Repositories

The main repository uses multiple sub-repositories to manage packages of
different categories. All packages are installed via the OpenWrt package
manager called `opkg`. If you're looking to develop the web interface or port
packages to OpenWrt, please find the fitting repository below.

* [LuCI Web Interface](https://github.com/openwrt/luci): Modern and modular
  interface to control the device via a web browser.

* [OpenWrt Packages](https://github.com/openwrt/packages): Community repository
  of ported packages.

* [OpenWrt Routing](https://github.com/openwrt/routing): Packages specifically
  focused on (mesh) routing.

* [OpenWrt Video](https://github.com/openwrt/video): Packages specifically
  focused on display servers and clients (Xorg and Wayland).

## Support Information

For a list of supported devices see the [OpenWrt Hardware Database](https://openwrt.org/supported_devices)

### Documentation

* [Quick Start Guide](https://openwrt.org/docs/guide-quick-start/start)
* [User Guide](https://openwrt.org/docs/guide-user/start)
* [Developer Documentation](https://openwrt.org/docs/guide-developer/start)
* [Technical Reference](https://openwrt.org/docs/techref/start)

### Support Community

* [Forum](https://forum.openwrt.org): For usage, projects, discussions and hardware advise.
* [Support Chat](https://webchat.oftc.net/#openwrt): Channel `#openwrt` on **oftc.net**.

### Developer Community

* [Bug Reports](https://bugs.openwrt.org): Report bugs in OpenWrt
* [Dev Mailing List](https://lists.openwrt.org/mailman/listinfo/openwrt-devel): Send patches
* [Dev Chat](https://webchat.oftc.net/#openwrt-devel): Channel `#openwrt-devel` on **oftc.net**.

## License

OpenWrt is licensed under GPL-2.0
