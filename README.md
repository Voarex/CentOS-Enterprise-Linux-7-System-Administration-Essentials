# CentOS Enterprise Linux 7 - System Administration Essentials
Inside this repository will be a tutorial for how to go from zero to hero on the essentials of CentOS Linux 7 System Administration.

## Table of Contents
1. [Prerequisites](#prereq)
   1. *[Having a basic understanding of System Administration](#pre-req)*
2. [Demo some tools](#demo-tools)
3. [Creating a lab](#lab-creation)
4. [Learning the Essentials of CentOS Enterprise Linux 7 Administration](#essentials)
5. [Installing CentOS Linux 7](#install-centos)
6. [Help and Archiving](#help)
7. [Working on CLI/Reading Files](#cli-read-files)
8. [Permission and Root Access](#permissions)
9. [Using Vi/Piping and Redirection](#vim-editor)
10. [SSH and Screen](#ssh-screen-login)  
  1.  [SSH CLIENTS](#ssh-screen-login)  
      1.  [Putty]()
      2.  [Windows 10 default command prompt]()
      3.  [Linux SSH]()
12. [Markdown](#md)

### Prerequisites <a name="prereq"></a>

 * *Having a basic understanding of System Administration is recommended for the Demo of basic tools, otherwise google is your best friend.*

### Demo some basic tools <a name="demo-tools"></a>

 *In this demonstration you will need to have an open lab, hence the basic knowledge of system administration. If you do not have a lab created, that's okay just continue to [Creating a lab](#lab-creation) portion of this repo. You can then continue on with the demo after if you'd like, or you can just jump right into the rest of the repository.*

 I will just start by showing some simple commands that you can use as well as in different types of scripting languages.

 1. By entering ```cat /etc/system-release``` on the CLI, you will see we are using CentOS Linux 7.9.2009. (Core) on the current system. The command ```cat``` is to display a file's contents.  
You can see below that there is only one line after the command entered.

  Display using shell
```shell
[cellis@master ~]$ cat /etc/system-release
CentOS Linux release 7.9.2009 (Core)
```

  Display using ruby
```ruby
[cellis@master ~]$ cat /etc/system-release
CentOS Linux release 7.9.2009 (Core)
```

  Display using python (Linux default language)
```python
[(username)@master ~]$ cat /etc/system-release
CentOS Linux release 7.9.2009 (Core)
```

  Display with no specific language attached, the basic CLI.  
  *I will be teaching you commands by using the basic CLI format.*
```
[(username)@master ~]$ cat /etc/system-release
CentOS Linux release 7.9.2009 (Core)
```


 2. Some fun shortcuts within the CLI: ```wc -l !$```  
This allows you to check the word count ```wc```, while also using the option newline ```-l```, and using our last argument ```!$```, which happens to be ```/etc/system-release```.

    * Below you will see the command under what you just typed, and the following line shows you the   option of newline ```-l``` for the file we previously searched for using ```cat```. Now as you see below we are using the word count function ```wc``` using option  ```-l``` to count the lines in the file, instead of counting the entire file's word count.
```
[cellis@master ~]$ wc -l !$
wc -l /etc/system-release
1 /etc/system-release
```
  Shown below you can see the entire ```wc``` of the ```/etc/system-release``` file including: bytes, characters and lines, but not in that order. The true order is as follows: newline, word, character, byte, maximum line length.
```
[cellis@master ~]$ wc /etc/system-release
  1  5 37  /etc/system-release
```


 3. If I want to check the date we can do that using the command ```date```.
```
[cellis@master ~]$ date
Fri Oct 1 03:57:58 EDT 2021
```
  * If you'd like to check a future date, you can use ```date --date "40 days"```.
```
Wed Nov 10 03:15:34 EST 2021
```  
  * If you'd like to check a past date, you can use ```date --date "40 days ago"```, etc.
```
Sun Aug 22 04:17:45 EDT 2021
```


 4. Typing ```cal``` on the CLI, you are able to see your calendar.
    * By entering ```cal -3``` you are able to get a 3 month range of the current months in calendar format.
    * By entering ```cal 7 1966``` you can see a specific date in calendar format.


 5. By entering ```python``` on the CLI and hit enter, you are able to do more complex math calculations as well as use python scripting. We will just use math for now.
```
[cellis@master ~]$ python
Python 2.7.5 (default, Nov 16 2020, 22:23:17)
[GCC 4.8.5 20150623 (Red Hat 4.8.5-44)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
  * If you'd like to see how many hosts you can have on your network you use python.  
  All you would do is use ```2``` to the power of ```**``` the amount of bits ```8``` minus 2 ```-2```. The amount of hosts we can have on the network is *254*, but if we squeeze some more bits out of the network ```>>> 2**12-2``` we can manage *4094*.
```
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
```
[cellis@master ~]$ tty
/dev/pts/0
```
   * If you want to see a long listing of this, you can type it all out if you like.
```
[cellis@master ~]$ ls -l /dev/pts/0
crw--w----. 1 cellis tty 136, 0 Oct  1 04:46 /dev/pts/0
```
   * Here we are using list `ls` then using `-l` for listing one file per line, known as long list. Then we use the ```$(tty)``` and this evaluates the tty command within the parenthesis that allows the path through to the device. Obviously this is shorter than typing the entire file.
```
[cellis@master ~]$ ls -l $(tty)
crw--w----. 1 cellis tty 136, 0 Oct  1 04:46 /dev/pts/0
 ```
  * If you look at the 2nd w shown here -> ```crw--(w)----```, this is the group write permissions.  
  What this means is that the group can write to my console, which really means anybody on the system write a message to my console.
```
crw--w----. 1 cellis tty 136, 0 Oct  1 04:46 /dev/pts/0
```
  * If we type the command messaging no -> ```mesg n```. This will disable the write permission for the group for this console.


### Creating a lab <a name="lab-creation"></a>

You will need to create a lab using a hypervisor. The most likely scenario is a free or open source software, but you can also use a closed source software if you're willing to pay and deal with certain support restrictions.

 #### Virtual Machine Hypervisors: <a name="hypervisor"></a>

 * ##### VirtualBox

 VirtualBox is an [open source software][software] that allows you to create a virtual machine.

 * ##### VMWare Fusion

  You may also use VMware Fusion. This is an Enterprise [closed source software][Fusion] also known as [proprietary software][Fusion].

 [software]: https://www.virtualbox.org/wiki/Downloads
 [Fusion]: https://www.vmware.com/products/fusion/fusion-evaluation.html

  * ##### KVM

  * ##### Red Had Hypervisor on KVM

  * ##### LXC

  * ##### LXD

  * ##### Docker

  * ##### Kubernetes

  * ##### Proxmox

  * ##### Citrix XenServer

  * ^ Coming soon...

### Learning the Essentials of CentOS Enterprise Linux 7 Administration <a name="essentials"></a>

### Installing Centos Linux 7 <a name="install-centos"></a>

### Help and Archiving <a name="help"></a>

### Working on the CLI/Reading Files <a name="cli-read-files"></a>

### Permissions and Root Access <a name="permissions"></a>

### Using Vi/Piping and Redirection <a name="vim-editor"></a>

### SSH and Screen <a name="ssh-screen-login"></a>

 * #### SSH CLIENTS <a name="clients"></a>

  * #### Putty <a name="putty"></a>

  * #### Windows 10 default command promp <a name="cmd"></a>

  * #### Linux SSH <a name="RedHat-SSH"></a>

### Markdown <a name="md"></a>
