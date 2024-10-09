---
title: "How to Set Up Vmmon and Vmnet Modules in VMware Workstation for Ubuntu"
seoTitle: "Install Vmmon and Vmnet Modules on Ubuntu"
seoDescription: "Guide to set up Vmmon and Vmnet modules in VMware Workstation on Ubuntu with step-by-step instructions"
datePublished: Wed Oct 09 2024 12:11:28 GMT+0000 (Coordinated Universal Time)
cuid: cm21twzkv00010ai5bt8e7xp3
slug: how-to-set-up-vmmon-and-vmnet-modules-in-vmware-workstation-for-ubuntu
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1728474729204/95b36103-2d8f-4c17-aa29-64cb9ce882f6.png
tags: cloud, ubuntu, devops, vmware, vmware-workstation

---

**Are you facing the below error when installing the vmware modules in Vmware workstation?**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728469329397/f98469fd-d19d-48b8-8acf-246bf5d38dce.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728469439397/b5923707-3cd8-4082-a33d-39c5fee04e79.png align="left")

I followed the instructions to install those modules from [this GitHub repo](https://github.com/mkubecek/vmware-host-modules).

1. **Find the vmware version installed**  
      
    To find version of the vmware installed, run the below command
    
    ```bash
    vmware -v
    ```
    
    It will show the output as
    
    ```bash
    VMware Workstation 17.5.0 build-22583795/code
    ```
    
    From the baove out the version of the vmware installed is **17.5.0**  
    
2. **Get the code form Github**  
      
    Go to [this github repository](https://github.com/mkubecek/vmware-host-modules) and `branches`, click the `all` tab. Search for the version you have installed like shown below.  
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728474090278/7ebe3ab3-6647-460a-99ff-3017369283b6.png align="center")
    
    Copy the branch name, and run the below command to get the source code into your system(Host).
    
    ```bash
    git clone -b branch-name https://github.com/mkubecek/vmware-host-modules.git
    ```
    
    Replace the *branch-name* with, you copied from github repository
    
3. Compile and Install  
      
    Go to directory vmware-host-modules like `cd cmware-host-modules`, And run the following two command. Make sure all VMs are stopped
    
    ```bash
    sudo make
    sudo make install
    ```
    
    Restart the vmware by using the below command
    
    ```bash
    sudo systemctl restart vmware
    ```
    
    Then, open the vmware it will work smoothly and won’t show the pop to install the moduels again.
    
    For more [visit this installtion](https://github.com/mkubecek/vmware-host-modules/blob/master/INSTALL) guide from the author