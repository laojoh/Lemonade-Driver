# Lemonade-Driver
FBCP-ILI9341 (ILI9488-Targetting) Driver for 4.0" SPI TFT LCD Display

# Background
For some context, this is a driver I spent hours trying to work out and find **specifically** for this screen, in the 4.0" no touch version: https://www.aliexpress.us/item/3256809575069193.html?spm=a2g0o.detail.0.0.604fhvjyhvjywW&mp=1&pdp_npi=6%40dis%21USD%21USD+13.32%21USD+0.99%21%21USD+0.99%21%21%21%402103212b17806555389702086ea6dd%2112000050079449351%21ct%21US%21-1%21%211%210%21&_gl=1*1mbfbkz*_gcl_au*MjgxNDYxOTA5LjE3Nzg1NTY1NzY.*_ga*MTgxOTI1OTc1Ni4xNzgwNjQzMjcx*_ga_VED1YSGNC7*czE3ODA2OTc5ODQkbzQkZzAkdDE3ODA2OTc5ODckajU3JGwwJGgw&gatewayAdapt=glo2usa

**please keep in mind that this driver is setup to be compatiblle with both the screen listed above and also a Raspberry Pi Zero 2 W. (RP02W)** (Not tested on other controllers such as pico, regular raspberry pis, or arduinos)

# Use
## Step 1
**Look at the display**

There should be 1x14 pins on the right side of the screen. If there isn't, return or exchange, as it could be defective. 


## Step 2
**Turn it around 180 deg**

The '4.0" TFT SPI 480x320 V1.1' text on the bottom is now on the top, upside down. Next to the pins, you should be able to read little labels, starting with 'VCC' on the bottom and so on. 


## Step 3
**Make clear to yourself the pins on the RP02W**

Go to this site: https://pinout.xyz and keep it open for future reference. 


## Step 4
**Start wiring**

Make sure to have female-female jumper wires, able to go on the pins. 

Next, we start wiring!

| Display Pin | RP02W Pin |
| --- | --- |
| VCC | Pin 1 (3.3V Power) |
| GND | Pin 9 (Ground) |
| CS | Pin 24 (GPIO 8 or SPI0 CE0) |
| RESET | Pin 22 (GPIO 25) |
| DC/RS | Pin 18 (GPIO 24) |
| SDI(MOSI) | Pin 19 (GPIO 10 or SPI0 MOSI) |
| SCK | Pin 23 (GPIO 11 or SPI0 SCLK) |
| LED | Pin 17 (3.3V Power) |

## Step 5
**Install OS**

Get a micro-SD card and download the Raspberry Pi Imager. Put the micro-SD into a larger adapter for a computer, and then insert it.

Once in the Raspberry Pi Imager, select:

Raspberry Pi Zero 2 W

Raspberry Pi OS **(Legacy, 32-bit)**

Your micro-SD

The name of your project **(Write down or remember well)**

Timezone, yada yada yada

Make a username and password **(Make sure to remember it or write it down, you will need it)**

The local network of your computer (name and password)

**Enable SSH should be turned ON, with password authentification**

Then, **Write**! (It might take a while) 

## Step 6
**SSH Into your Raspberry Pi**

Install PuTTY, it makes things easier. Trust me. 

Plug in your RP02W, and wait for the light to stay solid. Then, go into windows terminal and type

```
ping {insert project name (yes, the one you made)}.local
```

This will return an IP address, looking like a bunch of random numbers separated by colons. 

Now, assuming you have installed putty, in the terminal, type 

```
putty
```

This will open a new window of PuTTY, and you will then be prompter to enter an IP address. Take the IP address you just found, and enter it. 

If connected, it will open a PuTTY terminal, and that will prompt you to login with the username and password you made earlier. You're now in the RP02W!

## Step 7
**Installing things**

Once you're logged in, you will need to install some things. Run these commands:

```bash
sudo apt update
sudo apt install git
sudo apt install libraspberrypi-dev
sudo apt-get install cmake
```

This will get you set up with all the necessary things you need to get this screen to run.

Next,

```
git -v
```
To check if git has installed properly.

Then,
```
cd ~
git clone https://github.com/laojoh/Lemonade-Driver
```

## Step 8
**Running the screen**

Now, you should have everything installed, and I've already premade the build file for you.

Enter these commands:
```
cd Lemonade-Driver
cd build
sudo ./fbcp-ili9341
```

Hopefully, it should work! 

# Other things
