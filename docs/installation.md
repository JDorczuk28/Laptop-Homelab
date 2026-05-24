# Server Install

This Document covers the basic installation process to turn an old/broken laptop into an Ubuntu Server

## Goal

Install Ubuntu Server on a broken laptop and replace the existing Windows install so the laptop can be a dedicated server

## Media 

Downloaded Ubuntu 26.04 LTS ISO and used Rufus to create a bootable USB 
Used DD mode to write ISO to the USB Drive

## Booting From USB

The Laptop was booted from the USB installer from the boot menu
Once the server was installed the USB was no longer needed

## Setup

During installation, I chose to erase the internal drive and install Ubuntu Server as the only operating system.
This replaced the previous Windows installation.

During the Ubuntu Server installation, I selected the option to install OpenSSH Server
This allows the server to be managed remotely from another computer using:
```bash
ssh USERNAME@SERVER_IP
