# raspbian-headless
Raspbian Headless is a linux distribution for Raspberry Pi suitable for headless installation and deployment.

The goal is to provide a "downloader" for an image that can be flashed to a memory card and does not require a monitor, keyboard or mouse to start using your Raspberry Pi.

## Theory

By default the Raspbian distribution has disabled DHCP for eth0. SSH is also turned off. We need to modify the image so that eth0 (the Pi's lan interface) listens either for DHCP or falls back to a known static IP address so that we can connect to it using an ethernet cable.

## Usage

### Installation
You should be able to run the downloader from the host linux terminal like this

```
/bin/sh -c "$(curl -fsSL https://raw.githubusercontent.com/aphex3k/raspbian-headless/master/bin/download)"
```

If all goes well this will leave an image file in your current directory that is ready to be flashed onto an SD card.

### Connecting
After flashing, plug in the ethernet cable into your Pi and power it up

#### DHCP
If your network is providing a DHCP service an IP address will be automatically assigned and you can connect to your Raspberry Pi using SSH. See your DHCP lease table or admin interface for details on how to determine the assigned IP address or scan your network for new devices.

#### Fallback
Alternatively configure the host end of the ethernet cable to the following settings:

```
IP host: 192.168.23.1
Subnet: 255.255.255.0
```
and after about a minute the Raspberry Pi will stop waiting for a DHCP response and will **fall back** to the following settings:

```
IP headlesspi: 192.168.23.2
Subnet: 255.255.255.0
```

### Setup

Just follow your typical Raspberry Pi configuration (e.g. raspi-config, etc.)

## Caveats

If you connect your Raspberry Pi to a host computer make sure you use a crossover cable or the host provides a gigabit ethernet interface.

## License

This tool is released under the [GNU General Public License Version 3](https://github.com/aphex3k/raspbian-headless/blob/master/LICENSE).
