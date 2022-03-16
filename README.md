---
description: >-
  A guide for developers looking to deploy a Cardano node to a cloud instance or
  locally to something like a Raspberry Pi.
---

# Easy Node Deployment

This guide will also not contain a one-click-run script (even though that would be nice) because there are too many deviations and nuances to consider that the creation of such a script would be very time intensive and most probably unstable. Instead this guide will attempt to collate all the useful Dev-ops information needed to create a robust local development node.This collection of tutorials is designed to serve as a collation of information for the deployment of a Cardano node for development purposes.&#x20;

### What this guide is and isn't

This is not a "_How-To"_ guide for the creation of a stake pool or even a full block production node. Instead this guide serves as a collection of information for developers that would like to setup a synced Cardano node to be able to mint NFTs or use any of the `cardano-cli` functions.

Most of the available literature is geared towards Stake Pool Operators, and  not towards developers who just want a synced node to make use of the cli functions or interact with some of the other tools provided by IOHK that require a synced node.

### How to read this guide

We will probably be expanding this in the future to consider builds on other platforms. Below will be a list of pages dedicated as a guide to building on each platform.

{% content-ref url="easy-node-deployment/raspberry-pi-4-node.md" %}
[raspberry-pi-4-node.md](easy-node-deployment/raspberry-pi-4-node.md)
{% endcontent-ref %}

### How this guide was funded

The creation of this guide and the associated research was funded partly through a Project Catalyst Proposal. The link below will take you to the proposal (The rectangle that says Community). In order to see the proposal you have to be logged into IdeaScale (not my rule).

{% embed url="https://cardano.ideascale.com/c/idea/383959" %}
Catalyst Proposal
{% endembed %}

## Proposal Changes

Between our original proposal's submission and the actual creation of this guide, we realized that a number of our initial hopes were rather unfeasible or would introduce more hassle than what the time was worth. The deviations from our original proposal as well as the explanation for why are given below.

### All-in-One Script

When we started this process we had every intention of creating an all-in-one script that would allow us to go live with one click. We very quickly gave up on this idea. The biggest reason was quite simply error checking and troubleshooting.

For most of the steps, it is far easier to debug by sequentially runninmg through a number of steps, than trying to figure out where in the hundreds of lines of bash-script something broke.
