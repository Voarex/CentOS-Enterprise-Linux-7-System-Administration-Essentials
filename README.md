
# CentOS Enterprise Linux 7 - System Administration Essentials

Inside this repository will be a tutorial on how to go from zero to hero on the essentials of CentOS Enterprise Linux 7 System Administration. You will learn by following along, taking notes and using the same commands as I do.

## Table of Contents

1. [Prerequisites](#prereq)
   1. *[Having a basic understanding of System Administration](#prereq)*
   1. *[Having a basic understanding of Github](#github)*
   1. *[Having a basic understanding of Markdown](#md)*
2. [Demo some basic tools](#demo-tools)
   1. [Demo recap](#demo-recap)
3. [Creating a lab](#lab-creation)
   1. [Virtual Machine Hypervisors](#vmhypervisor)
      1. [Oracle VirtualBox](#oracle)
      2. [VMware Fusion](#vmware)
4. [Learning the Essentials of CentOS Enterprise Linux 7 Administration](#essentials)
   1. [Course Overview](#overview)
   1. [Installing CentOS Linux 7](#install-centos)
      1. [Downloading CentOS](#download-centos)
      2. [VirtualBox Networking](#virtualbox-network)
      3. [Installing from Media](#install-media)
      4. [Installing from Network](#install-network)
      5. [Configure CentOS 7 Networking](#configure-centos-network)
      6. [Installing X](#install-x)
      7. [Add Guest Additions](#guest-additions)
   1. [Help and Archiving](#help)
   1. [Working on CLI/Reading Files](#cli-read-files)
   1. [Permission and Root Access](#permissions)
   1. [Using Vi/Piping and Redirection](#vim-editor)
   1. [SSH and Screen](#ssh-screen-login)  
      1.  [SSH CLIENTS](#ssh-screen-login)  
          1.  [Putty](#putty)
          2.  [Windows 10 default command prompt](#cmd)
          3.  [Linux SSH](#redhat-ssh)

## Prerequisites <a name="prereq"></a>

1. <a name="prereq"></a> *Having a basic understanding of __[System Administration](https://victorops.com/blog/definitive-guide-for-being-a-system-administrator)__ is recommended for this repository and for the Demo, otherwise [Google](www.google.com) is your best friend.*

3. <a name="github"></a> *Having a basic understanding of __[Github](https://github.com)__ will be important if you are not familiar, but I feel that you are already acquainted since you are here at this repository.*

2. <a name="md"></a> *Having a basic understanding of __[Markdown](https://www.markdowntutorial.com/)__ is not required to your abilities on taking this course. It will be essential for you to take notes professionally and staying organized. This will also help you learn how to use [Markdown](https://www.markdowntutorial.com/) by repeatedly writing it by preparing you for an Enterprise level experience. Use Markdown tutorials online, it is quite easy to use.*

   *  Markdown is an essential text editor and there are different flavors of Markdown depending on what platform you're using. For example, using __shell__ commands on [Github](www.github.com) are called **console** commands.

   *  Below you can see a Markdown preview of this repository. I use [Atom](www.atom.io) text editor.
   <img src="https://media.giphy.com/media/NKPuru8WWScVQSo2CH/giphy.gif" width="600" height="300">

## Demo some basic tools <a name="demo-tools"></a>

In this demonstration you will need to have an open lab, and some basic knowledge of system administration. If you do not have a lab created, that's okay just continue to [Creating a lab](#lab-creation) portion of this repository. You can then continue on with the demo after if you'd like, or you can just jump right into the rest of the repo. I will begin by showing some simple commands that you can use as well as some different types of *languages*.

1.  By entering ```cat /etc/system-release``` on the CLI, you will see we are using CentOS Linux 7.9.2009. (Core) on the current system. The command ```cat``` is to display a file's contents. You can see below that there is only one line after the command entered.
    *  CLI using the __Shell__ language, in Github it's called __Console__.  
    I will be teaching you commands by using the "__console__" format on the CLI.
       ```console
       [cellis@master ~]$ cat /etc/system-release
       CentOS Linux release 7.9.2009 (Core)
       ```   
       *  CLI using the __Python__ language, which is Linux's default language.  
       There are other languages, but that's not what this crash course is for.  
          ```python
          [cellis@master ~]$ cat /etc/system-release
          CentOS Linux release 7.9 (Core)
          ```

2.  This is a fun shortcut within the CLI: ```wc -l !$```  
This allows you to check the word count ```wc```  
While also using the option newline ```-l```  
Then using our last argument ```!$```  
Which happens to be ```/etc/system-release```.
    *  Below you will see the command under what you just typed, and the following line shows you the   option of newline ```-l``` for the file we previously searched for using ```cat```. Now as you see below we are using the word count function ```wc``` using option  ```-l``` to count the lines in the file, instead of counting the entire file's word count.
       ```console
       [cellis@master ~]$ wc -l !$
       wc -l /etc/system-release
       1 /etc/system-release
       ```
       *  Shown below you can see the entire ```wc``` of the ```/etc/system-release``` file including: bytes, characters and lines, but not in that order.  
       The true order for `wc` is as follows:  newline, word, character, byte, maximum length.  
          *  newline ```-l```
          *  word ```-w```
          *  character ```-c```
          *  byte ```-b```
          *  maximum line length ```-L```
            ```console
            [cellis@master ~]$ wc /etc/system-release
            1  5 37  /etc/system-release
            ```

3.  If I want to check the date we can do that using the command ```date```.
    ```console
    [cellis@master ~]$ date
    Fri Oct 1 03:57:58 EDT 2021
    ```    
    *  If you'd like to check a future date, you can use ```date --date "40 days"```.
       ```console
       Wed Nov 10 03:15:34 EST 2021
       ```
      *  If you'd like to check a past date, you can use ```date --date "40 days ago"```  
      The same applies for time ```date --date "1 hour ago"```, etc.
         ```console
         Sun Aug 22 04:17:45 EDT 2021
         Fri Oct  1 02:57:45 EDT 2021
         ```

4.  Typing ```cal``` on the CLI, you are able to see your calendar.  
    *  By entering ```cal -3``` you are able to get a 3 month range of the current months in calendar format.  
    *  By entering ```cal 1 2021``` you can see any specific date in calendar format.


5.  By entering ```python``` on the CLI, you are able to do more complex math calculations as well as use python for scripting. We will just use it for math right now.
    ```console
    [cellis@master ~]$ python
    Python 2.7.5 (default, Nov 16 2020, 22:23:17)
    [GCC 4.8.5 20150623 (Red Hat 4.8.5-44)] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
    >>>
    ```
    *  If you'd like to see how many hosts you can have on your network you use python.  
    All you would do is use ```2``` to the power of ```**``` the amount of bits ```8``` minus 2 ```-2```. The amount of hosts we can have on the network is *254*, but if we squeeze some more bits out of the network ```>>> 2**12-2``` we can manage *4094*.
       ```console
       [cellis@master ~]$ python
       Python 2.7.5 (default, Nov 16 2020, 22:23:17)
       [GCC 4.8.5 20150623 (Red Hat 4.8.5-44)] on linux2
       Type "help", "copyright", "credits" or "license" for more information.
       >>> 2**8-2
       254
       >>> 2**12-2
       4094
       ```
       *  To exit python just use Ctrl + D for Windows and Left Command + D for OSX.  
       If you want to clear the screen you can type ```clear```, or you can use Ctrl + L.


6.  By entering ```tty```, this will show you what terminal you are connected to. I am remote accessing the system via a secure shell -> ssh pseudo terminal. This pseudo terminal device we are connected to is actually also a file in the file system.
    ```console
    [cellis@master ~]$ tty
    /dev/pts/0
    ```

    *  If you want to see a long listing of this, you can type it all out if you like.
       ```console
       [cellis@master ~]$ ls -l /dev/pts/0
       crw--w----. 1 cellis tty 136, 0 Oct  1 04:46 /dev/pts/0
       ```
    *  Here we are listing using `ls` then listing one file per line `-l`, known as long list.  
    If we use the ```$(tty)```, this evaluates the tty command within the parenthesis which allows the path through to the device. This is shorter than typing out the long list for the entire file ```ls -l /dev/pts/0```.
       ```console
       [cellis@master ~]$ ls -l $(tty)
       crw--w----. 1 cellis tty 136, 0 Oct  1 04:46 /dev/pts/0
       ```
    *  If you look at the 2nd w shown here -> ```crw--(w)----```, this is the group write permissions.  
    What this means is that the group can write to my console, which really means anybody on the system write a message to my console.
       ```console
       crw--w----. 1 cellis tty 136, 0 Oct  1 04:46 /dev/pts/0
       ```
    *  If we type the command messaging no -> ```mesg n```. This will disable the write permission for the group for this console. Follow this command by ```ls -l $(tty)``` to check the file after the command.
       ```console
       [cellis@master ~]$ mesg n
       [cellis@master ~]$ ls -l $(tty)
       crw-------. 1 cellis tty 136, 0 Oct  1 04:46 /dev/pts/0
       ```      
    *  As you can see above the write permission under the group was removed. Down below you can turn this function back on using ```mesg y```. Follow that up by using ```ls -l $(tty)``` to check the file.
       ```console
       [cellis@master ~]$ mesg y
       [cellis@master ~]$ ls -l $(tty)
       crw--w----. 1 cellis tty 136, 0 Oct  1 04:46 /dev/pts/0
       ```

* ### Demo Recap <a name="demo-recap"></a>

 We just demonstrated what using a lab environment looks like inside of a hypervisor. We will be using VirtualBox as our virtual machine hypervisor and installing CentOS Linux 7. You will learn content through demonstrations by following along and taking notes by using [Markdown](#pre-req).

## Creating a lab <a name="lab-creation"></a>

You will need to create a lab using a [Hypervisor](#vmhypevisor) and the most likely scenario is a free or open source software, but you can also use a closed source software if you're willing to pay for more stable features but deal with the certain support resolution restrictions.

 1.  This is where we will use your host machine to connect to your virtual machine. Usually this consists of the following machines; host machine that's using VirtualBox , the CentOS 7 master server, CentOS 7 GUI server1, and CentOS 7 CLI server2. The command line(CLI) server will be more useful to you than the graphical user interface(GUI) serve, because we will be using enterprise systems. Enterprise systems mainly consist of remote connections via the CLI.

 2.  The master system will really be of less use to you since you probably do not have a local web server setup and that requires an installation of CentOS 7 for the web server or ftp server. You can also mimic the same remote installs from a web server by looking at CentOS distributions that are available to download via mirror servers.

     *  Lab Environment Example. We are using our host machine that's uses a Virtual Machine [Hypervisor](#vmhypervisor) called [Oracle VirtualBox.](#oracle)  

        <img src="https://media.giphy.com/media/HdDIoY52LALZDGo2ey/giphy.gif" width="300" height="300">

 * ### Virtual Machine Hypervisors <a name="vmhypervisor"></a>

  A Virtual Machine Hypervisor is a software, firmware, or type of hardware that allows you to run or manage virtual machines. A computer in which runs one or more virtual machines is called a host machine and every virtual machine is a guest machine.

 * #### Oracle VirtualBox <a name="oracle"></a>
 [Oracle VirtualBox][software] is a free [open source software][open-source] that allows you to create virtual machines. Free as in free to use and free as in freedom, because it is open source. If you have finished installing and need to return to setting up your [VirtualBox Network, click here.](#virtualbox-network)  
<img src="https://media.giphy.com/media/jiLy1vKv0zUb7cJPs1/giphy.gif" width="100" height="100">

 * #### VMWare Fusion <a name="vmware"></a>
 You may also use [VMware Fusion][fusion]. This is an Enterprise [closed source software][closed-source] also known as [proprietary software.][proprietary]  
 <img src="https://media.giphy.com/media/1uTyPuFHZB36juP4Xt/giphy.gif" width="100" height="100">

 * #### KVM

 * #### Red Had Hypervisor on KVM

 * #### LXC

 * #### LXD

 * #### Docker

 * #### Kubernetes

 * #### Proxmox

 * #### Citrix XenServer

 * ^ All hypervisor information coming soon...

## Learning the Essentials of CentOS Enterprise Linux 7 Administration <a name="essentials"></a>

* ### Installing CentOS Enterprise Linux 7 Overview <a name="install-centos"></a> <a name="overview"></a>

 You may find that there are things that you may __*not*__ know that __*may*__ or may __*not*__ be mentioned here. That's okay because every hurdle is just a learning experience. I will have more courses to help you better understand __CentOS Enterprise Linux 7__, this course is just the Essential crash course. As we make our way through this portion of the repo you will be doing the following:  
 *__Downloading ISO files__  
 __VirtualBox Server creation__  
 __VirtualBox Networking__  
 __Installing CentOS 7 from local media__  
 __Installing CentOS 7 from the network__  
 __Both of our ISO installs will be minimal installs__  
 __Adding X Server GUI to Server 1__  
 __Install VirtualBox Guest Additions__*

* ### Downloading CentOS <a name="download-centos"></a>

  During our download of CentOS Linux 7, we will be able to install different types of CentOS as previously mentioned during the overview. We will be using a "Minimal" install for both of our servers because you can always scale up at a later date.

  *  If you go to [www.CentOS.org](https://www.centOS.org) you will be given choices with tabs at the top and the two buttons under [The CentOS Project](www.centos.org). We will choose the [CentOS Linux](https://centos.org/centos-linux/) button or click the [Download](https://centos.org/download/) tab.  
  ![CentOS.org](https://media.giphy.com/media/VmBRZik5Kxw3we4zLa/giphy.gif)

     *  Once you've chosen CentOS Linux, you will be shown a few options.  
     You will need to select the tab 7 (2009) and choose x86_64.  
     ![CentOS Linux 7](https://media.giphy.com/media/sE7tAOEVmTJXe2pqXa/giphy.gif)

        *  Once the __x86_64__ hyperlink has been chosen you will be presented with a list of mirrors to download your ISO that is available in your region.  
        ![CentOS x86_64](https://media.giphy.com/media/FdZPEYRFQflCdLl2tE/giphy.gif)

           *  Once you click the mirror hyperlink you will be shown ISO files to choose from. We will be choosing __CentOS-7-x86_64-Minimal-2009.iso__ download. The ISO list is as follows:  
           Everything DVD - All that CentOS can provide in 7GB+ download   
           DVD - 4GB Full Installation DVD  
           Minimal - A CD size install around 600MB, enough for a Minimal install of CentOS.  
           NetInstall - A download about ~10MB for a pure NetInstall.  
           ![Index of CentOS](https://media.giphy.com/media/218VGNfKFdxP7tsaYJ/giphy.gif)

* ### VirtualBox Networking <a name="virtualbox-network"></a>

  If you have not already installed [VirtualBox](#lab-creation), then you'll need to visit the [Creating a lab](#lab-creation) portion of this repo and install [Oracle VirtualBox](#lab-creation) for Windows, OSX, Linux, or Solaris.

  *  Now that you have downloaded [Oracle VirtualBox](#lab-creation) you will be setting up your NatNetwork settings. If you did not create a server don't worry you weren't supposed to. You will need to configure your network settings first. You technically can setup Network settings before or after, but it can be tricky either way, so pay attention and follow the instructions below to configure your NatNetwork.

     *  Click on Tools and click Preferences, you may also click File and preferences.  
     Ctrl + G or Left Command + G.  
     ![VirtualBox Preferences](https://media.giphy.com/media/0abmjDJ1ZMhH3v4OQq/giphy.gif)
        *  Click Networking.  
        ![VirtualBox Network](https://media.giphy.com/media/xemmReUK5GEh0kaK6r/giphy.gif)  
           *  Click the add new NAT network button and click Ok to continue with your new NatNetwork.  
           ![VirtualBox NAT Network](https://media.giphy.com/media/cWL4c9vsqvnmBxzxfJ/giphy.gif)

* ### Installing from Media <a name="install-media"></a>
  Here we will be installing from the physical media and adding a GUI to server1.

  *  Go ahead and click the blue button that says "New".  
  ![Oracle VirtualBox Manager](https://media.giphy.com/media/zTuHcSCCtACGhmfT2n/giphy.gif)

     *  You will now be prompted with naming your new virtual machine and choosing an operating system. I recommend just choosing the name "CentOS" and it automatically picks the operating system type as Linux and the version as Red Hat (64-bit). You can then just choose a different name like "server1" before continuing and it keeps the same OS as before. You may also just name the server and choose from the drop down list. Hit next, and continue with the default options as shown below, unless you specifically know what you are changing.  
     ![Oracle VirtualBox Manager](https://media.giphy.com/media/yr7TsUTcbV01vGuj1l/giphy.gif)

        *  Choose the following options to setup your VirtualBox:
           *  Choosing your memory size. Stick to defaults.  
           ![Oracle VirtualBox Storage](https://media.giphy.com/media/7AoRg5UqXkLWmDBoog/giphy.gif)
           *  Creating your Virtual Machine Hard disk. Stick to defaults.  
           ![Oracle VirtualBox Hard Disk](https://media.giphy.com/media/SCqWxn6AGo2CaXOtJr/giphy.gif)
           *  Choosing your Hard Disk file type. Stick to defaults.  
           ![Oracle VirtualBox Hard Disk Type](https://media.giphy.com/media/17s5qiFhCrYwU9bPPL/giphy.gif)
           *  Choosing your storage on the Hard Disk. Stick to defaults.  
           ![Oracle VirtualBox Hard Disk Storage](https://media.giphy.com/media/k0yzBmjwkHUfJgiWmN/giphy.gif)
           *  Choosing your file location and size. Stick to defaults.  
           ![Oracle VirtualBox File Location/Size](https://media.giphy.com/media/LPOiUFEzd0GX8GzkcL/giphy.gif)

  *  Server Storage steps are as follows:
     *  Left click on the server1 and choose Storage  
     ![server1 storage](https://media.giphy.com/media/fnIagfkWa5FLxmKf6O/giphy.gif)
     *  Choose Empty,  
     Choose the blue disk,  
     Choose/Create a Virtual Optical Disk...  
     ![server1 storage controller:IDE](https://media.giphy.com/media/1S2O2Q5fudJR4071d3/giphy.gif)
     *  Choose the Minimal install __CentOS-7-x86_64-Minimal-2009.iso__.  
     ![server1 iso-minial](https://media.giphy.com/media/c5sKUBS6gzy1nBXvy9/giphy.gif)

  *  Server Networking steps are as follows:
     *  Left click on the network under server1.  
     ![server1 Networking](https://media.giphy.com/media/trJc53B40JmEedJ0KB/giphy.gif)
     *  Click "Enable Network Adapter" if it is not enabled.  
     ![server1 Network Adapter 1](https://media.giphy.com/media/2fTjUBlc7Mu5mQF7sN/giphy.gif)  
     *  Click "Attached To:" and choose "NAT Network".  
     ![server1 Network Adapter 1](https://media.giphy.com/media/ASuKSldNd2zuYUEoh8/giphy.gif)
     *  Click "Name:" Choose "NatNetwork", the network we created from before and click "Ok".  
     ![server1 Network Adapter 1](https://media.giphy.com/media/EomdhYlekXyNyG8VEw/giphy.gif)
     *  Click on Adapter 2 click "Enable Network Adapter" if it is not enabled.  
     ![server1 Network Adapter 2](https://media.giphy.com/media/h5YFfKo7ANWQ2Qc8mC/giphy.gif)
     *  Click "Attached to:" and choose "Host-only Adapter".  
     ![server1 Network Adapter 2 ](https://media.giphy.com/media/GnPRpUQyaEknTC6tug/giphy.gif)
     *  Click "Name:" Choose "VirtualBox Host-only Ethernet Adapter", click "Ok".  
     ![server1 Network Adapter 2](https://media.giphy.com/media/wGBa0m4te4ESWDkn5e/giphy.gif)

  *  You may now start the server by pressing "Start"  
  ![server1 Start](https://media.giphy.com/media/TrJWqZhfSmSTXqbwlE/giphy.gif)
     *  Use the up arrow to highlight __Install CentOS 7__ and hit Enter.
     ![server1 Install](https://media.giphy.com/media/12DKfJeLdYG2MqB1ms/giphy.gif)
     *  Choose your language  
     ![server1 Language](https://media.giphy.com/media/ZpCSlbptR5M4PbuMCk/giphy.gif)
     *  Click "Installation Destination"  
     ![server1 Installation Destination](https://media.giphy.com/media/YILG2lvkvWp5qeBAa4/giphy.gif)
     *  Click "Done"  
     ![server1 Installation Destination Done](https://media.giphy.com/media/xdKwjPRAqENWa87IL2/giphy.gif)
     *  Click "Network & Host Name"  
     ![server1 Network & Host Name](https://media.giphy.com/media/cXzBTvSYDOwDNGDLil/giphy.gif)
     *  Enable both the Networks and Name the Host network  
     ![server1 Network & Host Name](https://media.giphy.com/media/Ty0MGlLOFU8eb3eVm7/giphy.gif)
     *  Click "Begin Installation"  
     ![server1 Begin Installation](https://media.giphy.com/media/jp7EcKOUyJCmPtEXTF/giphy.gif)
     *  Let's setup our Root Password. Root is the administrator user  
     ![server1 Root Password](https://media.giphy.com/media/taCP3pwKUacRDhgFUw/giphy.gif)
     *  Choose an easy password to remember, click "Done" twice  
     ![server1 Root Password Confirm](https://media.giphy.com/media/fPmAXNAkVsAB0rYvH5/giphy.gif)
     *  Now do the same for "User Creation"  
     ![server1 User Creation](https://media.giphy.com/media/d0AQSZnBbt25lhYVAG/giphy.gif)
     *  Leave the Full Name blank,  
     Enter your username,  
     add to Administration Wheel,  
     and choose a password.  
     Confirm by clicking "Done" twice  
     ![server1 User Password](https://media.giphy.com/media/nDNCsFyKN39r30doap/giphy.gif)
     *  Click Finish Config.  
     ![server1 Finish Config & Reboot](https://media.giphy.com/media/SOsPpdRhkJh9qtjMx1/giphy.gif)
     *  Click Reboot.  
     ![server1 Reboot](https://media.giphy.com/media/HUdDWmqKHNjFIKl8Hq/giphy.gif)
     *  Server Login - exit this and move to Installing from the Network.  
     ![server Login](https://media.giphy.com/media/eGitN42jaejwzdmeqX/giphy.gif)

*  ### Installing from the Network <a name="install-network"></a>
  Here we will be installing from the network, which is very similar to media. In fact, you follow the same first few steps. You will need to create and configure a new server and do all of the steps right until you have to start the server. This will be your server2. Mine may say server3, ignore that.

  *  You will need to configure another server and make the same steps up until before you start the server. You will now start the server by pressing "Start".  
  ![server2 Start](https://media.giphy.com/media/TrJWqZhfSmSTXqbwlE/giphy.gif)
     *  Use the up arrow to highlight __Install CentOS 7__ and hit Enter.
     ![server2 Install](https://media.giphy.com/media/12DKfJeLdYG2MqB1ms/giphy.gif)
     *  Choose your language  
     ![server2 Language](https://media.giphy.com/media/ZpCSlbptR5M4PbuMCk/giphy.gif)
     *  Click "Installation Destination"  
     ![server2 Installation Destination](https://media.giphy.com/media/YILG2lvkvWp5qeBAa4/giphy.gif)
     *  Click "Done"  
     ![server2 Installation Destination Done](https://media.giphy.com/media/xdKwjPRAqENWa87IL2/giphy.gif)
     *  Click "Network & Host Name"  
     ![server2 Network & Host Name](https://media.giphy.com/media/cXzBTvSYDOwDNGDLil/giphy.gif)
     *  Enable both the Networks and Name the Host network (server2.example.com)
     ![server2 Network & Host Name](https://media.giphy.com/media/Ty0MGlLOFU8eb3eVm7/giphy.gif)

     ###### NOW YOU ARE CAUGHT UP... and we can begin with the difference.

     * Choose "Installation Source".  
     ![server2 Installation Source](https://media.giphy.com/media/WmpL3VSADbtN2K4TDW/giphy.gif)
     * Select "On The Network", and you can use your mirror, or a local host i.e 192.168.56.220/centos7/ etc. Click Done.  
     ![server2 On The Network](https://media.giphy.com/media/3COO8NIa22fXrq1cjQ/giphy.gif)
     * You should be downloading the new package.  
     ![server2 OTN Downloading Package](https://media.giphy.com/media/ONDLiaEMi0Su7TCxLA/giphy.gif)
     * Choose "Software Selection".  
     ![server2 Software Selection](https://media.giphy.com/media/G2XQYOVbgBJkOVSwJL/giphy.gif)
     *  Click "Begin Installation"  
     ![server1 Begin Installation](https://media.giphy.com/media/7RxLBm2YF0gD79aHAv/giphy.gif)
     *  Let's setup our Root Password. Root is the administrator user  
     ![server1 Root Password](https://media.giphy.com/media/taCP3pwKUacRDhgFUw/giphy.gif)
     *  Choose an easy password to remember, click "Done" twice  
     ![server1 Root Password Confirm](https://media.giphy.com/media/fPmAXNAkVsAB0rYvH5/giphy.gif)
     *  Now do the same for "User Creation"  
     ![server1 User Creation](https://media.giphy.com/media/d0AQSZnBbt25lhYVAG/giphy.gif)
     *  Leave the Full Name blank,  
     Enter your username,  
     add to Administration Wheel,  
     and choose a password,  
     Confirm by clicking "Done" twice if your password is weak.  
     ![server1 User Password](https://media.giphy.com/media/nDNCsFyKN39r30doap/giphy.gif)
     *  Click Finish Config.  
     ![server1 Finish Config & Reboot](https://media.giphy.com/media/SOsPpdRhkJh9qtjMx1/giphy.gif)
     *  Click Reboot.  
     ![server1 Reboot](https://media.giphy.com/media/HUdDWmqKHNjFIKl8Hq/giphy.gif)
     *  Server Login - exit this and move back to server1.  
     ![server Login](https://media.giphy.com/media/eGitN42jaejwzdmeqX/giphy.gif)  

* ### Configure CentOS 7 Networking <a name="configure-centos-network"></a>

  * You will connect to server1 and login as root and you can connect to the VM using an SSH client if you like. Once connected to server1 you will insert the command: ```ip a s```, which stands for IP Address Show.      
    ```
    [root@server1 ~]# ip a s
    ```   
    ![server configure networking ip](https://media.giphy.com/media/Rsz09sygeL9BajMUXz/giphy.gif)  

  * If you are not seeing the address you can CTRL + L (Clear) and use ```nmcli conn show```, looking at the results we can see the connections we have.
    ```
    [root@server1 ~]# nmcli conn show
    ```   
    ![server configure networking ip connections](https://media.giphy.com/media/GKkCPaBN7vtMDBystC/giphy.gif)

  * If one of those connections isn't up or isn't showing us our IP address we can do ```nmcli conn up enp0s3``` and ```nmcli conn up enp0s8``` to bring both interfaces up if they aren't.
    ```
    [root@server1 ~]# nmcli conn up enp0s3
    ```  
    ```
    [root@server1 ~]# nmcli conn up enp0s8
    ```   
    ![server1 configure networking ip connections](https://media.giphy.com/media/GKkCPaBN7vtMDBystC/giphy.gif)

  * You can do ```ip a s``` to verify they are connected to the network. However we need to make sure this happens all the time.  
    ```
    [root@server1 ~]# ip a s
    ```   
    ![server configure networking ip](https://media.giphy.com/media/ZmuC9XTbsQGbQjDBL1/giphy.gif)

  * In order to make sure the connections are verified all the time, we need to do some commans under root very carefully. The command we are going to run is CASE SENSITIVE. We will run sed for stream editing and -i for in-place edits, and s/ searching for the string. The forward slashes separate: ```sed -i s/ONBOOT=no/ONBOOT=yes/ /etc/sysconfig/network-scripts/ifcfg-enp0s3```. If you use tab complete for most of your directories it will autocomplete ensuring less mistakes are made. Forward slashes are our path separator. Using the Up arrow key you can do the same for the enpo0s8, by removing the 3 and replacing with the 8. ```sed -i s/ONBOOT=no/ONBOOT=yes/ /etc/sysconfig/network-scripts/ifcfg-enp0s8```. We can search the text within a file using ```grep```. ```grep ONBOOT !$``` !$ for the last argument, and then up arrow and repeat for both ```grep ONBOOT /etc/sysconfig/netwwork-scripts/ifcfg-enp0s3```.
    ```  
    [root@server1 ~]# sed -i s/ONBOOT=no/ONBOOT=yes/ /etc/sysconfig/network-scripts/ifcfg-enp0s3
    [root@server1 ~]# sed -i s/ONBOOT=no/ONBOOT=yes/ /etc/sysconfig/network-scripts/ifcfg-enp0s8
    [root@server1 ~]# grep ONBOOT !$
    grep ONBOOT /etc/sysconfig/network-scripts/ifcfg-enp0s8
    ONBOOT=yes
    [root@server1 ~]# grep ONBOOT /etc/sysconfig/network-scripts/ifcfg-enp0s3
    ONBOOT="yes"
    [root@server1 ~]#
    ```  
    ![server1 configure networking onboot](https://media.giphy.com/media/pzLwJlEQhwfjBKVMXL/giphy.gif)


*  ### Installing X <a name="install-x"></a>
   Here we will still be connected to server1 as root. We will be installing x.

   * We will check for updates using the command ```yum update``` you can also run ```yum update -y``` if you don't want to manually accept the packages you are updating to.
     ```
     [root@server1 ~]# yum update -y
     ```
     ![server1 yum update](https://media.giphy.com/media/tkDGtpR3UVM0ZVlU7t/giphy.gif)

   * We will now add some additional software. We are going to run ```yum install -y``` using the ```-y``` so we don't accept prompts to continue. We will separate any packages by using a space as it's the default separator within the command line shell. We will be installing ```redhat-lsb-core``` and also ```net-tools``` that are common packages we can use all the time. We will include ```epel-release``` which will put on a new software repository. This will allow us to access the MATE desktop graphical environment we want to use. It's important to do ```yum update``` first because of the ```kernel-headers``` to ensure they match the kernel and the headers for the development tools we will get. We need ```kernel-devel``` devel for development. This is the driver and software for the guest additions. The entire command is: ```yum install -y redbat-lsb-core net-tools epel-release kernel-headers kernel-devel```
     ```
     [root@server1 ~]# yum install -y redbat-lsb-core net-tools epel-release kernel-headers kernel-devel
     ```
     ![server1 yum install](https://media.giphy.com/media/l6bl7UefcvkpCSTIaa/giphy.gif)  
     After completion  
     ![server1 yum install complete](https://media.giphy.com/media/FqceGtmGeNnbmlcNMN/giphy.gif)

   * Now that you have completed you can clear the screen ctrl + L and we are going to be installing a group of packages. The command ```yum groupinstall -y "Development Tools"``` is a groupinstall and the quotes exist because there is a space in the group name. This is for when we are installing the virtualbox additions, we will need tools from this. Enter that command and hit enter.
     ```
     [root@server1 ~]# yum groupinstall -y "Development Tools"
     ```
     ![server1 groupinstall Dev Tools](https://media.giphy.com/media/VSM8mrgWgO8fk9axV3/giphy.gif)

   * Server1 is our graphical machine and we need to install the desktop using ```yum groupinstall -y "X Window System" "MATE Desktop"```. This is case sensitive. We want to put on the MATE Desktop and it's a simple desktop meant for a server environment. It still has a lot of software, but it's the simple minimal install first to work from the CLI and then we can add the packages faster after starting from a minimal install. We only need this on our server1 because we want to make sure our graphical environment is setup before we install our guest additions.
     ```
     [root@server1 ~]# yum groupinstall -y "X Window System" "MATE Desktop"
     ```
     ![server1 groupinstall packages](https://media.giphy.com/media/a5qtJ1MMfu817rMPCy/giphy.gif)

   * We now need to make the system use the newly installed packages. We will use ```systemctl``` the service management tool and set the default ```set-default``` to the run level which is known as the ```graphical.target```.
     ```
     [root@server1 ~]# systemctl set-default graphical.target
     ```
     ![server1 systemctl](https://media.giphy.com/media/upUwVXofc4BdY5C90P/giphy.gif)

   * Now we need to make sure we enter that environment using the ```isolate``` command to take us through to our graphical target ```systemctl isolate graphical.target```. Once you are completed we will do some similar tasks with server2, but nothing regarding the graphical interface.
     ```
     [root@server1 ~]# systemctl isolate graphical.target
     ```
     ![server1 systemctl isolate](https://media.giphy.com/media/drrOiJKF8mkrVHGxCK/giphy.gif)

     You will know you completed it when it looks like this.
     ![server1 graphical environment](https://media.giphy.com/media/DCGHEvxzjFQ7mtujRW/giphy.gif)

*  ### Add Guest Additions <a name="guest-additions"></a>
   We will now be installing the guest additions on our server1 and on both ideally. Especially for the graphical machine, this will allow you to display graphics and go into a full-screen mode and cut/paste. If you are in the virtual machine and want to leave you need to his the Host Key. For windows its the Right Ctrl Button, but for OSX it's Left Command Key. Let's reboot the virtual machine by going to the top right and clicking the power button > restart.  
   ![server1 add guest additions restart](https://media.giphy.com/media/lu93Vd5Ez4lptgvBiH/giphy.gif)

   *

*  ### Help and Archiving <a name="help"></a>

*  ### Working on the CLI/Reading Files <a name="cli-read-files"></a>

*  ### Permissions and Root Access <a name="permissions"></a>

*  ### Using Vi/Piping and Redirection <a name="vim-editor"></a>

*  ### SSH and Screen <a name="ssh-screen-login"></a>

  *  #### SSH CLIENTS <a name="clients"></a>

     *  ##### Putty <a name="putty"></a>

     *  ##### Windows 10 default command promp <a name="cmd"></a>

     *  ##### Linux SSH <a name="redhat-ssh"></a>

<a name="definitions"></a>

[software]: https://www.virtualbox.org/wiki/Downloads
[open-source]: https://en.wikipedia.org/wiki/Open-source_software
[proprietary]: https://en.wikipedia.org/wiki/Proprietary_software
[closed-source]: https://en.wikipedia.org/wiki/Proprietary_software
[fusion]: https://www.vmware.com/products/fusion/fusion-evaluation.html
