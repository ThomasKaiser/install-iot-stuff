# install-iot-stuff

A non interactive version of Pete Scargill's http://tech.scargill.net/a-christmas-script/

## Design goal

This script should be a replacement for Pete Scargill's 'The script' easing the installation of a lot of IoT related software packages. Target platforms are those supported by Armbian and Raspbian (Ubuntu Xenial, Debian Jessie and soon Stretch both `armhf` and `arm64`).

While installation process and priorities (eg. security) might differ the installation result should be the same as when using Pete's script so that the loads of tutorials and information on scargill.net can be used. Also every installation routine will be contained in an own function so that Pete&Team can decide whether they adopt functions or not.

This small project will also serve as test platform regarding performance on 64-bit boards with constrained memory and some potential performance optimizations (eg. not limiting Node-RED to 128MB DRAM as it might be necessary on the smallest Raspberries but adjusting the amount of memory by something like `--max-old-space-size=$(( $(free | awk -F" " '/^Mem:/ {print $2}') / 3096 ))`

**Differences**

- non-interactive mode, to install eg Node-RED and Webmin it's a `sudo install-iot-stuff nodered webmin` (this is necessary to automate installations further or to even integrate this into OS image creation)
- the script should be called with `sudo` to prevent *credential caching* timing out if it has to run on very slow SD cards or installations with low network/internet connectivity. For non-privileged stuff `su ${SUDO_USER}` will be used while the main task runs as superuser
- the requirement to have a `pi` user living in `/home/pi/` has to be removed
- no security weakening, Debian/Ubuntu distro policies should an can remain intact

**Status**

Nothing yet, still preparing test environment, waiting for dev board samples and doing some basic research (eg. [using 32-bit NodeJS/V8 on 64-bit systems](https://github.com/nodesource/distributions/issues/375#issuecomment-290393891))
