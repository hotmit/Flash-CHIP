# What changed in this repo
* Added old & compatible platform tools
* Upgrade to Debian 9 

## Flash
```
Follow the original instruction below

Once done, connect the composite tv input. Use the cred below
User: root
Pw: chip (default)

# type this in the shell to change network settings
nmtui (use this to set ur wifi password) 
```

## Change Source List
[Ref](http://chip.jfpossibilities.com/chip/debian/)
```
sudo nano /etc/apt/sources.list
find: deb http://opensource.nextthing.co/chip/debian/repo jessie main
    replace with: deb http://chip.jfpossibilities.com/chip/debian/repo jessie main
    
sudo nano /etc/apt/preferences
    Replace with: (3 lines below)
        Package: *
        Pin: origin chip.jfpossibilities.com
        Pin-Priority: 1050
        
sudo apt update          
```

## Upgrade to Debian Sketch
[Ref](https://yoursunny.com/t/2019/bye-CHIP/)
[Kernel Build Script](https://github.com/kaplan2539/CHIP-Debian-Kernel)
```
Copied from the build script in the ref link above:
    # Add this repository
    wget -qO - https://kaplan2539.github.io/CHIP-Debian-Kernel/PUBLIC.KEY | sudo apt-key add -
    echo "deb http://kaplan2539.github.io/CHIP-Debian-Kernel jessie main" | sudo tee --append /etc/apt/sources.list
    sudo apt-get update
    
    # Install the new kernel
    sudo apt-get install linux-image-4.4.138-chip rtl8723bs-mp-driver-modules-4.4.138 chip-mali-modules-4.4.138
    

# upgrade the packages after kernel upgrade
nano etc/apt/sources.list
    Change every jessie to stretch.
    Delete jfpossibilities and kaplan2539 repositories, as they do not provide packages for Debian Stretch.
    
# finally run the upgrade command
sudo apt update
sudo apt full-upgrade 
```

# Helpful Links
* [Archive Page](https://archive.org/details/C.h.i.p.FlashCollection)
* [Original Chrome Tool + Images 1.7GB](http://chip.jfpossibilities.com/flash-chrome/)
* [Pihole Ads blocking with CHIP](https://docs.pi-hole.net/main/basic-install/)


---
---
---
# Flash-CHIP
Ready to use Flash environment for the C.H.I.P Single Board Computer

Simplyfies the Flashing Process for the C.H.I.P and PocketC.H.I.P Computer. 

## Instructions
1. Remove the C.H.I.P from its case (in case you have a Pocket C.H.I.P).
2. Connect the FEL and a GROUND pin of the C.H.I.P (for example, with a paperclip).
3. Connect the C.H.I.P its micro USB port to a USB port of your Linux machine.
4. In the Linux machine:
    - run ` git clone https://github.com/thore-krug/Flash-CHIP.git` to clone this repository.
    - `cd` into the location where you stored this repository.
    - run `sudo chmod +x Flash.sh`
    - run `./Flash.sh`
    - Select the version you want to install.
    - Wait until the installation finishes.
    - Enjoy!
  
## Troubleshooting 
### General Issues
1. Kill the Script with ctrl + C 
2. Read the output if something is not installed or Permissions are missing 
3. Just restart the Script (fixes most of the Problem with FEL and Fastboot ) 
4. If this does not help reboot, retry
5. Open an Issue on this Git Repo. 

### The script times out waiting for fel
This error is related to an insufficient amount of power provided by your USB port to the C.H.I.P.  
If you have an external `5V` power supply, you can connect it to the `CHG-IN` pin of your C.H.I.P. to provide sufficient power.    
Alternatively try a different (shorter, or higher quality) USB cable and check if your host PC has USB power saving enabled.  

If this dos not work Install sunxi-tool v1.4.1:
```bash
sudo apt install libusb-1.0-0-dev libz-dev libfdt-dev

git clone --branch v1.4.2  https://github.com/linux-sunxi/sunxi-tools.git
cd sunxi-tools/
make install-all install-misc
cd ../
./Flash.sh
```
## Support my work by Donating 

https://www.paypal.me/a13tech (the original developer)
