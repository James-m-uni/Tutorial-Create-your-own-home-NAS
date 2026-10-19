# Create your own home NAS
This tutorial will show you how to create your own home NAS that you can use to store your files.

## Is a NAS storage solution right for me?
To decide if a NAS storage solution is the right thing for you, you first have to question why you need a NAS over other
storage solutions such as a third-party cloud storage provider like OneDrive or iCloud. 

### Advantages
| Cloud Storage                                             | Home NAS                                                                |
|-----------------------------------------------------------|-------------------------------------------------------------------------|
| Large storage options available                           | More granular control over security                                     |
| Can connect from any computer with an internet connection | Can add very large hard drives to your setup without a high monthly fee |
| Dont have to worry about hosting                          | Do not have to pay for an extra susbcription to a cloud storage service |

### Disadvantages
| Cloud Storage                                                               | Home NAS                                                                                                                               |
|-----------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| Monthly subscription required                                               | You are responsible for the security                                                                                                   |
| Your data is stored in a companies servers where they are at risk of attack | Requries an extra device in your house to always be on                                                                                 |
| Trusting third-party company data encryption standards and rules            | Requies more setup                                                                                                                     |
|                                                                             | You are responsible for backups of the contents ON the NAS                                                                             |
|                                                                             | Can only access the drive on your HOME network <br/>unless you install software to allow access from remote locations (e.g. Tailscale) |

## Required hardware
This setup requires a Raspberry Pi (preferably 3 or higher), a SATA hard drive and a USB to SATA converter.

## Initial setup
For this setup I will be using a Raspberry Pi 5 with a 2TB hard drive. 

<img src="/img/rpi5.png">

The USB to SATA adapter you choose depends on what size of hard drive you choose. A larger 3.5"
SATA hard drive requires more power compared to a 2.5" hard drive. Thus it would be beneficial to purchase a SATA adapter which has its own power source. If you are choosing
a smaller 2.5" hard drive, you can use a direct adapter as there isn't an extra power need.

SSDs dont require as much power as a HDD, so you will be fine using a direct adapter.

Since we are hosting the storage from an external storage device, we don't need to buy a large SD card. For my setup, I will use a 64gb SD card for the OS image.

For reliable speeds, you should connect your Raspberry Pi/computer to your home network/Router via Ethernet.

First you need to download an operating system on your Raspberry Pi. I am going to use the Raspberry Pi OS. Download the OS imager from the Raspberry Pi website <a href="https://www.raspberrypi.com/software/">here</a>.

This software allows you to create an OS image directly onto your SD card.

## Setup OS
After imaging the OS, find a permanent place for the Raspberry Pi to live (preferably somewhere with good ventilation and has a route for a cable to run from the RPi to the Router).

Set up the RPi, connecting power and a keyboard/mouse temporarily and follow on screen OS setup instructions until you reach the desktop.

Take note of the Username and Password you chose when setting up the OS. (You must have a password!)

## Enable SSH
For you to easily control the RPi, you need to enable SSH so you can control the computer from the terminal at any other computer connected to the same network.

The setup process is different for every different OS, but the process for Raspberry Pi OS is as shown below:

1. Open the terminal and enter ```sudo raspi-config```
2. Navigate to <i>Interface Options</i> and press enter
3. Find <i>SSH</i> then press enter - following on-screen instructions to enable SSH.
4. Exit raspi-config

## Set up the external storage device
If the storage drive isn't connected to your RPi yet, connect it now.

We need to format and mount our external device.

1. In the terminal, type ```sudo lsblk``` (This shows all the storage devices connected to your RPi).
2. Identify what label your storage device is by looking at the storage capacity of each connected drive. In my case, it is sdb.
3. We now need to format the drive. Enter ```sudo fdisk /dev/sdb``` replacing <b>sdb</b> with whichever label your drive was under.


