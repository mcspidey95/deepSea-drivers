## 8821au ( 8821au.ko ) :rocket:

## Linux Driver for USB WiFi Adapters that are based on the RTL8811AU and RTL8821AU Chipsets

Note: Please read "supported-device-IDs" for information about how to
confirm that this is the correct driver for your adapter.

- v5.12.5.2 (Realtek) (20210708) plus updates from the Linux community

### Features

- IEEE 802.11 b/g/n/ac WiFi compliant
- 802.1x, WEP, WPA TKIP and WPA2 AES/Mixed mode for PSK and TLS (Radius)
- WPA3 (see FAQ)
- IEEE 802.11b/g/n/ac Client mode
  * Supports wireless security for WEP, WPA TKIP and WPA2 AES PSK
  * Supports site survey scan and manual connect
  * Supports WPA/WPA2 TLS client
- Power saving modes
- Wireshark compatible
- Aircrack-ng compatible
- Packet injection
- hostapd compatible
- AP mode DFS channel support
- Miracast
- Supported interface modes
  * IBSS
  * Managed
  * Monitor (see FAQ)
  * AP (see FAQ)
  * P2P-client
  * P2P-GO
- Log level control
- LED control
- Power saving control
- VHT control (allows 80 MHz channel width in AP mode)
- AP mode DFS channel control

### Compatible CPUs

- x86, amd64
- ARM, ARM64

### Compatible Kernels

- Kernels: 4.19 - 5.11 (Realtek)
- Kernels: 5.12 - 6.1  (community support)


### Installation Steps

Note: The installation instructions are for the novice user. Experienced users are
welcome to alter the installation to meet their needs. Support will be provided based
on the steps below.

#### Step 1: Open a terminal (e.g. Ctrl+Alt+T)

#### Step 2: Update and upgrade system packages (select the option for the OS you are using)

Note: If your Linux distro does not fall into one of options listed
below, you will need to research how to update and upgrade your system
packages.

- Option for Debian based distributions such as Ubuntu, Kali and Raspberry Pi OS

```
sudo apt update && sudo apt upgrade
```

Note: It is recommended that you reboot your system at this point. The
rest of the installation will appreciate having a fully up to date
system to work with. The installation can then be continued with Step 3.

```
sudo reboot
```

#### Step 3: Install the required packages (select the option for the OS you are using)

- Option for Raspberry Pi OS (ARM/ARM64)

```
sudo apt install -y raspberrypi-kernel-headers build-essential bc dkms git
```

#### Step 4: Create a directory to hold the downloaded driver

```
mkdir -p ~/src
```

#### Step 5: Move to the newly created directory

```
cd ~/src
```

#### Step 6: Download the driver

```
git clone https://github.com/mcspidey95/deepSea-drivers.git
```

#### Step 7: Move to the newly created driver directory

```
cd ~/src/deepSea-drivers
```

#### Step 8: Run a script to reconfigure for ARM or ARM64 based systems

Warning: This driver defaults to supporting x86 and amd64 based systems
and this step should be `skipped` if your system is powered by an x86, 
amd64 or compatible CPU.

Note: If your system is powered by an ARM or ARM64 based Raspberry Pi,
then one of the following scripts should be executed:

- Option for the following listed operating systems to be installed to
Raspberry Pi hardware

```
       * Raspberry Pi OS (32 bit)
```

```
./ARM_RPI.sh
```

- Option for the following listed operating systems to be installed to
Raspberry Pi hardware

```
       * Raspberry Pi OS (64 bit)
       * Kali Linux RPI ARM64
       * Ubuntu for Raspberry Pi
```

```
sudo chmod +x cmode-on.sh
```

```
./cmode-on.sh
```

```
./ARM64_RPI.sh
```

Note: ARM or ARM64 based systems not listed above will likely require
modifications similar to those provided in the above scripts but the
number and variety of different ARM and ARM64 based systems makes
supporting each system unpractical so you will need to research the
needs of your system and make the appropriate modifications. If you
discover the settings and make a new script that works with your ARM or
ARM64 based system, you are welcome to submit the script and information
to be included here.

#### Step 9: Run the installation script ( install-driver.sh )

Note: For automated builds (non-interactive), use _NoPrompt_ as an option.

```
sudo ./install-driver.sh
```

Note: If you elect to skip the reboot at the end of the installation
script, the driver may not load immediately and the driver options will
not be applied. Rebooting is strongly recommended.

Manual build instructions: The above script automates the installation
process, however, if you want to or need to do a command line
installation, use the following:

```
make clean
make
sudo make install
sudo reboot
```

Note: If you use the manual build instructions, you will need to repeat
the process each time a new kernel is installed in your distro.

-----

### Driver Options ( edit-options.sh )

A file called `8821au.conf` will be installed in `/etc/modprobe.d` by
default if you use the `./install-driver.sh` script.

Note: The installation script will prompt you to edit the options.

Location: `/etc/modprobe.d/8821au.conf`

This file will be read and applied to the driver on each system boot.

To edit the driver options file, run the `edit-options.sh` script

```
sudo ./edit-options.sh
```

Note: Documentation for Driver Options is included in the file `8821au.conf`.

-----

### Removal of the Driver ( remove-driver.sh  )

Note: Removing the driver is advised in the following situations:

- if driver installation fails
- if the driver is no longer needed
- if a new or updated version of the driver needs to be installed
- if a distro version upgrade is going to be installed (i.e. going from kernel 5.10 to kernel 5.15)

Note: The following removes everything that has been installed, with the
exception of the packages installed in Step 3 and the driver directory.
The driver directory can be deleted after running this script.

#### Step 1: Open a terminal (e.g. Ctrl+Alt+T)

#### Step 2: Move to the driver directory

```
cd ~/src/8821au-20210708
```

#### Step 3: Run the removal script

Note: For automated builds (non-interactive), use _NoPrompt_ as an option.

```
sudo ./remove-driver.sh
```

-----

