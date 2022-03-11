---
description: >-
  A guide for developers wanting to setup a Cardano node for development
  purposes using a Raspberry Pi 4. This guide is not a How-to for starting a
  stake pool!
---

# Raspberry Pi-4 Node

> _Don't worry, setting up a regular node is easy -_ Nobody (2022)

![Revelar's 3-Pi Testing Cluster](<../../.gitbook/assets/20220302\_185036 cropped.jpg>)

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
{% endhint %}

{% hint style="info" %}
We recommend that you get an NVME SSD as it greatly increases the speed of storage
{% endhint %}

## Raspbian OS Setup

Before we can do anything we first need to setup the operating system on our Raspberry Pi 4. There are many ways to go about this, for simplicity's sake, we just went with the standard Raspbian OS.

### Download the Raspberry Pi Imager

This is the tool we will use to load an operating system onto the Pi. This tool can be downloaded from [raspberrypi.com](https://www.raspberrypi.com/software/)





