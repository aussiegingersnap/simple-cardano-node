---
description: >-
  A guide for developers wanting to setup a Cardano node for development
  purposes using a Raspberry Pi 4. This guide is not a How-to for starting a
  stake pool!
---

# Raspberry Pi-4 Node

> _Don't worry, setting up a regular node is easy -_ Nobody (2022)

![Revelar's 3-Pi Testing Cluster](<../.gitbook/assets/20220302\_185036 cropped.jpg>)

## Introduction

At Revelar, we very quickly realized we needed to have some kind of development sandbox to write and test on-chain code. Being that we're also a bunch of hardware nerds, we decided to build a 3 Pi cluster and add RGB. \
As we went through the process of setting up a Cardano node, we encountered a lot of difficulty mostly because all of the information for our use case, was fragmented and spread out everywhere. \
So this guide presents all the information needed to setup a cardano-node on a Pi 4 to create a development platform.

So if you are looking for a guide to setup a Cardano node on a Raspbian based Pi 4 for the purpose of doing development or _cardano-cli_ tasks, then this is the right guide.

## Catalyst Proposal Corrections

The stuff that we changed from our proposal we put here.

## Hardware Prerequisites

* Raspberry Pi 4 8GB 64-bit
* Heat-sink with a fan ([Something like this](https://www.amazon.com/Raspberry-Armor-Metal-Aluminium-Heatsink/dp/B07VWM4J4L))
* Type C Power Supply
* NVME M.2 SSD with at least 256gb
* NVME M.2 to USB3.0 Case
* Ethernet Cable (If not using wifi)
* Computer Mouse, Keyboard and monitor

{% hint style="warning" %}
As of the date of writing, we have only created a node on a Raspberry Pi 4 with 8GB of RAM. Most literature online will also advise you to use an 8GB Pi so we suggest you also get an 8GB version.

You also REQUIRE a heatsink for the Raspberry Pi. One of the steps in this tutorial overclocks the Pi and for that you do NEED a heatsink. We recommend a single piece unit with an integrated fan.
{% endhint %}

{% hint style="info" %}
We recommend that you get an NVME SSD as it greatly increases the speed of storage
{% endhint %}

## OS Setup

Before we can do anything we first need to setup the operating system on our Raspberry Pi 4. There are many ways to go about this, for simplicity's sake, we just went with the standard Raspbian OS.

### Download the Raspberry Pi Imager

This is the tool we will use to load an operating system onto the Pi. This tool can be downloaded from [raspberrypi.com](https://www.raspberrypi.com/software/).&#x20;

### Download Raspberry Pi OS 64-bit

In this guide, we will use the standard Raspberry Pi OS. The OS can be downloaded from the official site.

{% embed url="https://www.raspberrypi.com/software/operating-systems#raspberry-pi-os-64-bit" %}
Raspberry Pi OS Download Location
{% endembed %}

Scroll down on the website and download the `Raspberry Pi OS with Desktop.` The picture below shows the latest version as at the time of writing. You may need to download a newer version if it is available.

![Raspberry Pi OS Download Screen](<../.gitbook/assets/Raspberry Pi OS.PNG>)

Once downloaded, extract the file into an empty folder. You should now have a disc image file in that file titled something like `2022-01-28-raspios-bullseye-arm64.img`.

### Flash the OS

Now connect your NVME SSD via USB and open Raspberry Pi Imager.&#x20;

![Sreenshot of the Raspberry Pi Imager interface](<../.gitbook/assets/raspberry pi imager.PNG>)

The Imager will have three options to choose from. Under _Operating System,_ scroll down the list and choose the `Use Custom` option. In the popup navigate to the Disc Image file we downloaded in the previous step.

![Option to select](<../.gitbook/assets/use custom.PNG>)

Next, select the name of your drive under the Storage option. Lastly click on _Write_ to start the process of writing an OS to the SSD. You will be asked to erase all data on disk to which you must say Yes.&#x20;

Now you just wait for the process to complete. It usually takes a couple of minutes.

## Raspberry Pi Setup

Once you have loaded an OS, you are ready to start with booting up your Pi. For the first time, you will require a keyboard, mouse and monitor to be directly connected to the Pi.

Make sure the Pi is now pluged in. Connect the HDMI, keyboard, mouse and SSD. Then only power it on. Give it a minute or two to read the OS from the SSD. Once done, navigate through the prompts. For sake of brevity I won't add screenshots here, as the prompts are pretty self explanatory however the general process is as follows.

1. Once you have booted into the OS, you will have a popup saying something to the effect _Welcome to Raspberry Pi..._ This is the start ofthe setup wizard so click next.
2. Set Country, language and Timezone
3. Change the Password for the default Pi user. This is your own preference although we strongly recommend you do change the password.
4. Setup the Screen
5. Connect to WiFi (or Ethernet in which case you simply skip)
6. Update Software (This is optional although you can skip this as we will be doing it later on anyways)
7. Restart the Pi

<details>

<summary>Issues we Encountered</summary>

#### HDMI Output not working

If the HDMI output does not appear to be working after the Pi has been powered on, switch the HDMI cable to the second HDMI port. During the setup of our cluster we found that HDMI port closest to the Type-C port, would not work during the first setup.

</details>

### Setting up VNC (Optional)

If you would like to access your Pi remotely from the same network, follow these steps to enable VNC access.

Open the Start Menu (Pi Logo in the top left), navigate to the Preferences tab and select the _Raspberry Pi Configuration_ option.

You should see the Raspberry Pi Configuration GUI.

Under the System Tab, you can change Auto login if you want. Since this is a development machine, this feature comes down to preference so choose whichever option you are more comfortable with.

Under the Display tab, disable Screen Blanking and choose the Headless Resolution that you want to see when you access the Pi remotely.

Under Interfaces tab, enable VNC. Alternatively you could use SSH. If you want to setup SSH, [here are the official docs ](https://www.raspberrypi.com/documentation/computers/remote-access.html#setting-up-an-ssh-server)on how to do so with a Pi.

Once all the options are set, reboot the Pi.

Once you have completed a reboot and logged into the Pi again. In the corner of the Taskbar you should now have a VNC logo. Click on it to open the VNC screen. [Here is a tutorial](https://discover.realvnc.com/blog/how-to-setup-vnc-connect-raspberry-pi) for how to connect to VNC.

## Update the Pi

Open a terminal and run the following command to update the software on the Pi.

```
sudo apt update && sudo apt full-upgrade
```

Once completed run the following two commands to clean up any temporary files created during the update process.

```
sudo apt autoremove && sudo apt autoclean
```

#### Configure Auto Updates (Optional)

You can configure the Pi to automatically install new security updates using the `unattended-upgrades` package. This is not a required step.

First install the required package (if it isn't installed already).

```
sudo apt install unattended-upgrades
```

Then configure it using the command below.

```
sudo dpkg-reconfigure -plow unattended-upgrades
```

## Overclock the Pi

{% hint style="danger" %}
Do not do this step if you do not have a heatsink installed! Overclocking a Pi without a heatsink could lead to thermal damage!
{% endhint %}

The Raspberry Pi 4 can safely be overclocked to run at 2GHz and that is the highest we will go in this guide. By safely we mean the resultant overclocked Pi is stable and does not void the warranty.

{% hint style="warning" %}
Overclocking the Pi 4 beyond 2GHz is possible, however it will void your warranty. If you want to overclock beyond 2GHz, do your own research!
{% endhint %}

To overclock we need to edit the `/boot/config.txt` file. You can use any text editor to do so, I use nano

```
sudo nano /boot/config.txt
```

Scroll down to the following lines:

```
#uncomment to overclock the arm. 700 MHz is the default.
#arm_freq=800
```

Just below this add in the following:

```
over_voltage=6
arm_freq=2000
```

Save the file (Ctrl-S & Ctrl-X), and reboot the Pi.

```
sudo reboot
```

## Harden the Pi

This is a very important step for those looking to run a Stake-pool. The intent of this guide is to setup a node for development and testing purposes, as such we will not go through all the steps to harden the Pi to become the most secure device known to man. If you do however want to harden your Pi [here is a great guide](https://raspberrytips.com/security-tips-raspberry-pi/) and [Here is another guide](https://gist.github.com/lokhman/cc716d2e2d373dd696b2d9264c0287a3) with ways to harden Ubuntu (which also work on Raspberry Pi.&#x20;

### Secure shared memory

The shared memory allows programs to communicate with one another through the RAM. By default this is enabled to be both read and write. In this step we will convert this shared memory to be read only. This prevents memory exploits.

To do this we need to edit `/etc/fstab.`

```
sudo nano /etc/fstab
```

To edit, append the following to the end of the file

```
tmpfs /run/shm tmpfs ro,noexec,nosuid 0 0
```

