---
title: "AWS VPC Peering and NAT Gateway!"
date: "2022-11-10"
description: &desc "Everything I learnt about VPC and NAT Gateways"
summary: *desc
tags: ["personal"]
showToC: true
---

## Terminology

Let us start with a few keywords and their meanings before we dip ourselves into networking.  
*The definitions are purposely boiled down to something very generic and understandable, but this is networking and things can get really complicated really fast, if you want to know them in-depth, I have added a few resources below*

1. **Virtual Private Cloud(VPC)**: tries to simulate a private network or a private cloud
2. **Subnet**: A *logical* subdivision of a network(Break a bigger network into smaller networks)
3. **Subnet Mask**: The dreaded `/24`. A string on 1s in a network IP address(in binary of course).
When it comes to an IP address, **192.168.54.69** for example.  
**192** is your **country**  
**168** is your **state**  
**54** is your **city**  
**69** is your **home**  
And when your subnet is `/24`, you're basically saying that 192.168.54 will never change, meaning you can have different homes but country, state, and city will be the exact same for every home.  
*Don't go for `/24` unless you know what you're doing, go for `/16`*
4. **Internet Gateway**: The gateway to ~~heaven~~ internet from the VPC.
5. **Route Table**: Set of rules to instruct where the network traffic should go to and/or come from.
6. **NAT Gateway**: One way ticket to either the internet or another subnet
7. **Peering VPCs**: Establishing connection between two VPCs so they can use eachother.
8. **Classless Inter-Domain Routing(CIDR)**: Basically subnet masking but the representation is cooler, like `/24` above.

## VPC

### Background

What VPCs are and why we need them

### VPC Setup

## Resources

1. Subnetting Tutorial - [Subnetting](https://www.subnetting.net/Tutorial.aspx)
2. CIDR Blocks/Notation - [Wikipedia](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation)
