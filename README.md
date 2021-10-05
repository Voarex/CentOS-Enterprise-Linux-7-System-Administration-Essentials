# CentOS Enterprise Linux 7 - System Administration Essentials

 * Inside this repository will be a tutorial on how to go from zero to hero on the essentials of CentOS Enterprise Linux 7 System Administration.


## Table of Contents
1. [Prerequisites](#prereq)
   1. *[Having a basic understanding of System Administration](#prereq)*
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
      3. [VirtualBox Server](#virtualbox-server)
      4. [Installing from DVD](#install-dvd)
      5. [Installing from Network](#install-network)
      6. [Adding the GUI](#gui)
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

 1. *Having a basic understanding of __[System Administration](https://victorops.com/blog/definitive-guide-for-being-a-system-administrator)__ is recommended for this repository and for the Demo, otherwise [Google](www.google.com) is your best friend.* <a name="prereq"></a>

 2. *Having a basic understanding of __[Markdown](www.markdowntutorial.com)__ is not required to your abilities on taking this course. It will be essential to you for taking notes professionally and staying organized. This will also help you learn how to use [Markdown](www.markdowntutorial.com) by repeatedly writing it.*  

   * Markdown is an essential text editor and there are different flavors of Markdown depending on what platform you're using. For example, using shell commands on Github are called console commands.

   * Below you can see a Markdown preview of this repository. I use [Atom]()
    ![Markdown](https://media.giphy.com/media/NKPuru8WWScVQSo2CH/giphy.gif)


## Demo some basic tools <a name="demo-tools"></a>

 * In this demonstration you will need to have an open lab, and some basic knowledge of system administration. If you do not have a lab created, that's okay just continue to [Creating a lab](#lab-creation) portion of this repository. You can then continue on with the demo after if you'd like, or you can just jump right into the rest of the repo. I will begin by showing some simple commands that you can use as well as some different types of *languages*.

 1. By entering ```cat /etc/system-release``` on the CLI, you will see we are using CentOS Linux 7.9.2009. (Core) on the current system. The command ```cat``` is to display a file's contents.  
You can see below that there is only one line after the command entered.

  * CLI using the Shell language, in Github it's called console.  
  I will be teaching you commands by using the *console* format.
```console
[cellis@master ~]$ cat /etc/system-release
CentOS Linux release 7.9.2009 (Core)
```
  * CLI using the Python language, which is Linux's default language.
```python
[(username)@master ~]$ cat /etc/system-release
CentOS Linux release 7.9.2009 (Core)
```

  * There are other languages, but that's not what this crash course is for.


 2. This is a fun shortcut within the CLI: ```wc -l !$```  
This allows you to check the word count ```wc```, while also using the option newline ```-l```, and using our last argument ```!$```, which happens to be ```/etc/system-release```.

  * Below you will see the command under what you just typed, and the following line shows you the   option of newline ```-l``` for the file we previously searched for using ```cat```. Now as you see below we are using the word count function ```wc``` using option  ```-l``` to count the lines in the file, instead of counting the entire file's word count.
```console
[cellis@master ~]$ wc -l !$
wc -l /etc/system-release
1 /etc/system-release
```
  * Shown below you can see the entire ```wc``` of the ```/etc/system-release``` file including: bytes, characters and lines, but not in that order.  
  The true order for `wc` is as follows:  newline, word, character, byte, maximum length.  
     * newline ```-l```  
     * word ```-w```  
     * character ```-c```  
     * byte ```-b```  
     * maximum line length ```-L```               
```console
[cellis@master ~]$ wc /etc/system-release
  1  5 37  /etc/system-release
```
 3. If I want to check the date we can do that using the command ```date```.
```console
[cellis@master ~]$ date
Fri Oct 1 03:57:58 EDT 2021
```
  * If you'd like to check a future date, you can use ```date --date "40 days"```.
```console
Wed Nov 10 03:15:34 EST 2021
```  
  * If you'd like to check a past date, you can use ```date --date "40 days ago"```, the same applies for time ```date --date "1 hour ago"```, etc.
```console
Sun Aug 22 04:17:45 EDT 2021
Fri Oct  1 02:57:45 EDT 2021
```
 4. Typing ```cal``` on the CLI, you are able to see your calendar.
    * By entering ```cal -3``` you are able to get a 3 month range of the current months in calendar format.
    * By entering ```cal 1 2021``` you can see any specific date in calendar format.


 5. By entering ```python``` on the CLI, you are able to do more complex math calculations as well as use python for scripting. We will just use it for math right now.
```console
[cellis@master ~]$ python
Python 2.7.5 (default, Nov 16 2020, 22:23:17)
[GCC 4.8.5 20150623 (Red Hat 4.8.5-44)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
  * If you'd like to see how many hosts you can have on your network you use python.  
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
  To exit python just use Ctrl + D for Windows and Left Command + D for OSX.  
  If you want to clear the screen you can type ```clear```, or you can use Ctrl + L.


 6. By entering ```tty```, this will show you what terminal you are connected to. I am remote accessing the system via a secure shell -> ssh pseudo terminal. This pseudo terminal device we are connected to is actually also a file in the file system.
```console
[cellis@master ~]$ tty
/dev/pts/0
```
   * If you want to see a long listing of this, you can type it all out if you like.
```console
[cellis@master ~]$ ls -l /dev/pts/0
crw--w----. 1 cellis tty 136, 0 Oct  1 04:46 /dev/pts/0
```
   * Here we are listing using `ls` then listing one file per line `-l`, known as long list.  
    If we use the ```$(tty)```, this evaluates the tty command within the parenthesis which allows the path through to the device. This is shorter than typing out the long list for the entire file ```ls -l /dev/pts/0```.
```console
[cellis@master ~]$ ls -l $(tty)
crw--w----. 1 cellis tty 136, 0 Oct  1 04:46 /dev/pts/0
 ```
* If you look at the 2nd w shown here -> ```crw--(w)----```, this is the group write permissions.  
  What this means is that the group can write to my console, which really means anybody on the system write a message to my console.
```console
crw--w----. 1 cellis tty 136, 0 Oct  1 04:46 /dev/pts/0
```
* If we type the command messaging no -> ```mesg n```. This will disable the write permission for the group for this console. Follow this command by ```ls -l $(tty)``` to check the file after the command.
```console
[cellis@master ~]$ mesg n
[cellis@master ~]$ ls -l $(tty)
crw-------. 1 cellis tty 136, 0 Oct  1 04:46 /dev/pts/0
```  
* As you can see above the write permission under the group was removed. Down below you can turn this function back on using ```mesg y```. Follow that up by using ```ls -l $(tty)``` to check the file.
```console
[cellis@master ~]$ mesg y
[cellis@master ~]$ ls -l $(tty)
crw--w----. 1 cellis tty 136, 0 Oct  1 04:46 /dev/pts/0
```

 ### Demo Summary <a name="demo-recap"></a>
  1. We were able to see how we use a lab environment inside a hypervisor. We will be using VirtualBox as our virtual machine and installing CentOS 7.9
  2. As you can see you will learn with demonstrations by following along with a summary at the end of each category to touch up the subject.

## Creating a lab <a name="lab-creation"></a>

1. You will need to create a lab using a hypervisor and the most likely scenario is a free or open source software, but you can also use a closed source software if you're willing to pay for more stable features but deal with the certain support resolution restrictions.

   * This is where we will use your host pc to connect to your virtual machine. Usually this consists of a few machines; Host System Using VirtualBox , the CentOS 7 master server, CentOS 7 GUI server1 server, and CentOS 7 CLI server2 server. The command line(CLI) will be more useful for you than the graphical user interface(GUI) since we will be using enterprise systems. That means those systems consist mainly of remote connections via the CLI.  The master system will really be of less use to you since you probably do not have a local web server setup and that requires an installation of CentOS 7 for the web server or ftp server. You can also mimic the same remote installs from a web server by looking at CentOS distributions that are available to download via mirror servers.
   * Lab Environment Example. We are using a Host System with a hypervisor called [Oracle VirtualBox](#oracle).
![Lab Environment](https://media.giphy.com/media/HdDIoY52LALZDGo2ey/giphy.gif)

    ### Virtual Machine Hypervisors: <a name="vmhypervisor"></a>

    * ##### Oracle VirtualBox <a name="oracle"></a>

      [Oracle VirtualBox][software] is an free [open source software][open-source] that allows you to create a virtual machine. Free as in free to use. Free as in freedom, because it is open source so it isn't restricted.  
      If you have finished installing and need to return to setting up your [VirtualBox Network, click here](#virtualbox-network).  

      ![VirtualBox](https://media.giphy.com/media/jiLy1vKv0zUb7cJPs1/giphy.gif)

    * ##### VMWare Fusion <a name="vmware"></a>

      You may also use [VMware Fusion][fusion]. This is an Enterprise [closed source software][closed-source] also known as [proprietary software][proprietary].  

      ![VmWareFusion](https://media.giphy.com/media/1uTyPuFHZB36juP4Xt/giphy.gif)

    * ##### KVM

    * ##### Red Had Hypervisor on KVM

    * ##### LXC

    * ##### LXD

    * ##### Docker

    * ##### Kubernetes

    * ##### Proxmox

    * ##### Citrix XenServer

    * ^ All hypervisor information coming soon...

## Learning the Essentials of CentOS Enterprise Linux 7 Administration <a name="essentials"></a>

* ### Installing Centos Enterprise Linux 7 Overview <a name="install-centos"></a> <a name="overview"></a>

  * As we make our way through this portion of the repository you will be doing the following:  
  Downloading ISO files  
  VirtualBox Networking  
  Installing CentOS 7 from local media  
  Installing CentOS 7 from the network  
   - Local Web server  
   - [www.CentOS.org](https://CentOS.org)
   - http://mirrors.vcea.wsu.edu/centos/7.9.2009/isos/x86_64/ - ISO Mirror example  

   Both of our ISO installs will be minimal installs  
   Adding X Server GUI to Server 1  
   Install VirtualBox Guest Additions

  * You may find that there are things that you may *not* know that may or may not be mentioned here. That's okay because every hurdle is just a learning experience. I will have more courses to help you better understand CentOS ENTerprise Linux 7, this course is just the Essential crash course.


* #### Downloading CentOS <a name="download-centos"></a>

 * During our download of CentOS Linux 7, we will be able to install different types of CentOS as previously mentioned during the overview. We will be using a minimal install for both of our servers because you can always scale up.


* If you go to [www.CentOS.org](https://www.centOS.org) you will be given choices with tabs at the top and the two buttons under The CentOS Project. We will choose the [CentOS Linux](https://centos.org/centos-linux/) button or click the [Download](https://centos.org/download/) tab.  
![CentOS.org](https://media.giphy.com/media/VmBRZik5Kxw3we4zLa/giphy.gif)

 * Once you've chosen CentOS Linux, you will be shown a few options.  
 You will need to select the tab 7 (2009) and choose x86_64.   
 ![CentOS Linux 7](https://media.giphy.com/media/sE7tAOEVmTJXe2pqXa/giphy.gif)  
 * Once the x86_64 hyperlink has been chosen you will be presented with a list of mirrors to download your ISO that is available in your region.  
 ![CentOS x86_64](https://media.giphy.com/media/FdZPEYRFQflCdLl2tE/giphy.gif)

 * Once you click the mirror hyperlink you will be shown ISO files to choose from. We will be choosing CentOS-7-x86_64-Minimal-2009.iso download. The ISO list is as follows:  
 Everything DVD - All that CentOS can provide in 7GB+ download   
 DVD - 4GB Full Installation DVD  
 Minimal - A CD size install around 600MB, enough for a Minimal install of CentOS.  
 NetInstall - If you look through this link you can find AltArch Releases. Which is about ~10MB for a pure NetInstall.  
 ![Index of CentOS](https://media.giphy.com/media/218VGNfKFdxP7tsaYJ/giphy.gif)

* #### VirtualBox Server Creation <a name="virtualbox-server"></a>

 * Go ahead and click the blue button that says "New".  
 ![Oracle VirtualBox Manager](https://media.giphy.com/media/zTuHcSCCtACGhmfT2n/giphy.gif)

 * You will now be prompted with naming your new virtual machine and choosing an operating system. I recommend just choosing the name "CentOS" and it automatically picks the operating system type as Linux and the version as Red Hat (64-bit), then you can just choose a different name before continuing and it keeps the OS. You may also just name the server and choose from the drop down list. Then hit next, and continue with the default options as shown below, unless you specifically know what you are changing.
 ![Oracle VirtualBox Manager](https://media.giphy.com/media/yr7TsUTcbV01vGuj1l/giphy.gif)
   - Default options for setting up your VirtualBox Server are as follows:  
   ![]()
   ![]()
   ![]()




* #### VirtualBox Networking <a name="virtualbox-network"></a>

 * If you have not already installed [VirtualBox](#lab-creation), then you'll need to visit the [Creating a lab](#lab-creation) portion of this repo and install [Oracle VirtualBox](#lab-creation) for Windows, OSX, Linux, or Solaris.

 * Now that you have downloaded [Oracle VirtualBox](#lab-creation) you will be setting up your Nat Network and Host-only Adapter. Since you will not have a starting server, you will need to configure your Network information or you can also do this after creating your server. It can be tricky either way so pay attention!  
 Follow the instructions below to configure your NatNetwork.  
   - Click Preferences.  
   ![VirtualBox Preferences](https://media.giphy.com/media/0abmjDJ1ZMhH3v4OQq/giphy.gif)
   - Click Networking.  
   ![VirtualBox Network](https://media.giphy.com/media/xemmReUK5GEh0kaK6r/giphy.gif)
   - Click the add new NAT network button and click Ok to continue with your new NatNetwork.  
   ![VirtualBox NAT Network](https://media.giphy.com/media/cWL4c9vsqvnmBxzxfJ/giphy.gif)

* #### Installing from DVD <a name="install-dvd"></a>

* #### Installing from the Networking <a name="install-network"></a>

* #### Adding the GUI <a name="gui"></a>

* #### Add Guest Additions <a name="guest-additions"></a>

* ### Help and Archiving <a name="help"></a>

* ### Working on the CLI/Reading Files <a name="cli-read-files"></a>

* ### Permissions and Root Access <a name="permissions"></a>

* ### Using Vi/Piping and Redirection <a name="vim-editor"></a>

* ### SSH and Screen <a name="ssh-screen-login"></a>

  * ### SSH CLIENTS <a name="clients"></a>

  * ##### Putty <a name="putty"></a>

  * ##### Windows 10 default command promp <a name="cmd"></a>

  * ##### Linux SSH <a name="redhat-ssh"></a>

## Markdown <a name="md"></a>


[software]: https://www.virtualbox.org/wiki/Downloads
[fusion]: https://www.vmware.com/products/fusion/fusion-evaluation.html
[open-source]: https://en.wikipedia.org/wiki/Open-source_software
[proprietary]: https://en.wikipedia.org/wiki/Proprietary_software
[closed-source]: https://en.wikipedia.org/wiki/Proprietary_software
