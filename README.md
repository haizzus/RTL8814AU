# Realtek RTL8814AU USB WiFi Driver

Driver for the Edimax EW7833UAC (AC1750 802.11ac Dual-Band Wi-Fi USB 3.0 Adapter), TP-Link Archer T9UH (AC1900 802.11ac Dual-Band Wi-Fi USB 3.0 Adapter) and other adapters using the same Realtek chipset.
Modified from the original source code for Linux kernels up to 4.8 with DKMS support.
Should work on modern Linux kernels from 4.9 to 4.16.

## Usage
I recommend to install driver using DKMS, since it will make sure to recompile driver once you install newer kernel and generally requires less manual work.

### Installation
You'll need to have `git` and `dkms` packages on you machine, which on Debian (based) systems (like Ubuntu) is done like this:
```bash
sudo apt-get install git dkms
```

Next clone this repository onto your machine somewhere:
```bash
git clone https://github.com/nazar-pc/RTL8814AU.git
```

Now go to the directory with cloned driver and install it using DKMS:
```
cd RTL8814AU
sudo ./dkms-install.sh
```

### Removal
If you later on want to remove this driver, just go to the directory with cloned driver and remove DKMS driver:
```
sudo ./dkms-remove.sh
```

### From https://github.com/astsam/rtl8812au
for setting monitor mode

    Set interface down
```
$ sudo ip link set wlan0 down
```
    Set monitor mode
```
$ sudo iwconfig wlan0 mode monitor
```
    Set interface up
```
$ sudo ip link set wlan0 up
```
for switching channels (interface must be up)

Set channel 6, width 40 MHz:
```
$ sudo iw wlan0 set channel 6 HT40-
```
Set channel 149, width 80 MHz:
```
$ sudo iw wlan0 set freq 5745 80 5775
```
for setting TX power (v4.3.21 branch only):
```
$ sudo iwconfig wlan0 txpower 30
```
or
```
$ sudo iw wlan0 set txpower fixed 3000
```
to inject frames with b/g rates use the Rate field in the radiotap header

to inject frames with n rates use the MCS field in the radiotap header

to inject frames with ac rates use the VHT field in the radiotap header
