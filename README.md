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

### How this guide was funded

The creation of this guide and the associated research was funded partly through a Project Catalyst Proposal. The link below will take you to the proposal. In order to see the proposal you have to be logged into IdeaScale (not my rule).

{% embed url="https://cardano.ideascale.com/c/idea/383959" %}
Catalyst Proposal
{% endembed %}

{% hint style="info" %}
If you do not know what Project Catalyst is, follow the embed below to the Catalyst website
{% endhint %}

