---
layout: post
title:  "How to Install Ubuntu on VirtualBox: A Step-by-Step Guide"
date:   2024-11-10
---

<p>A great way to explore Linux without affecting your main operating system is running Ubuntu on VirtualBox. Whether you’re a developer, student or just someone curious about Ubuntu, this guide will show you how to set it up on VirtualBox.</p>

#### System Requirements
<p>Before setting up Ubuntu on VirtualBox, ensure your computer meets the following requirements:</p>

   * **Processor:** 2 GHz dual-core processor
   * **RAM:** 8 GB or more (4 GB for your host OS and at least 4 GB for Ubuntu)
   * **Storage:** At least 25 GB free for the virtual machine
   * **Virtualization:** Make sure virtualization is enabled in your BIOS/UEFI settings.

#### Downloading and Installing VirtualBox
First, you need to install VirtualBox on your machine:
   1. Go to the VirtualBox website and download the latest version for your operating system.
   2. Once the installer is downloaded, run the setup and follow the instructions to install VirtualBox.
   3. After installation, open VirtualBox. You’ll now be ready to create your virtual machine for Ubuntu.

#### Downloading Ubuntu
   1. Go to the official Ubuntu website and download the latest Ubuntu Desktop version (choose either 24.04 LTS or 22.04 LTS, depending on your preference).
   2. Save the ISO file on your computer. This file will be used to install Ubuntu on your virtual machine.

<img src="/assets/img/ubuntu.png" alt=""> 

#### Setting Up Ubuntu on VirtualBox

##### Step 1: Creating a New Virtual Machine
   1. Open VirtualBox and click the **New** button to create a new virtual machine.
   2. Name your virtual machine “Ubuntu” or any name you prefer.
   3. Select **Linux** as the type and choose **Ubuntu (64-bit)** as the version.

<img src="/assets/img/Ubuntu0.png" alt="">

#### Configure system resources
   1. **Memory (RAM):** Assign at least 4 GB (4096 MB) of RAM for your Ubuntu VM. If your system has more RAM available, you can    allocate more for better performance.
   2. **Hard Disk:** Choose Create a virtual hard disk now and click Create.

   * Select **VDI (VirtualBox Disk Image)** as the hard disk type.
   * Choose **Dynamically allocated** for storage allocation (this allows the disk to expand as needed).
   * Set the disk size to at least 25 GB and click **Create.**

<img src="/assets/img/Ubuntu1.png" alt="">

<img src="/assets/img/Ubuntu2.png" alt="">

### Installing Ubuntu
   * Select your new virtual machine and click **Start.**
   * Click **Start** to boot the virtual machine from the Ubuntu ISO.
   * Choose **Try Ubuntu** or **Install Ubuntu.** If you want to explore Ubuntu before installing, you can select Try Ubuntu, but for the installation, choose **Install Ubuntu.**
   * **Select Keyboard Layout:** Choose your preferred keyboard layout and click **Continue.**
   * Choose between **Default Selection** (with more software like browsers, office tools, and media players) or **Extended Selection** (just the essentials).

### Installation Type
* Select **Erase disk and install Ubuntu.** Don’t worry — this will only affect the virtual hard disk you created, not your physical computer.

<img src="/assets/img/Ubuntu3.png" alt="">

* Click Next
* Fill in your credentials to create your account.
* Select your timezone, Click **Install Now** and confirm the changes.

Once the installation finishes, you'll be prompted to restart your virtual machine.

<img src="/assets/img/Ubuntu4.png" alt="">

After restarting, remove the Ubuntu ISO from the virtual drive by going to **Devices > Optical Drives > Remove Disk from Virtual Drive,** and press **Enter** to boot into your new Ubuntu environment.

Running Ubuntu on VirtualBox is an excellent way to experience Linux without changing your main operating system. Whether you’re testing out new features or learning Linux for the first time, VirtualBox provides a flexible and risk-free environment to work in.