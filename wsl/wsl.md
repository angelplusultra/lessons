# WSL (Windows Subsystem for Linux)

### What is WSL?

WSL stands for Windows Subsystem for Linux

The Windows Subsystem for Linux lets developers run a GNU/Linux environment -- including most command-line tools, utilities, and applications -- directly on Windows, unmodified, without the overhead of a traditional virtual machine or dualboot setup.

Every windows machine with Windows 10+ has the ability to run WSL

### Why Use A Linux Environment over Windows?

- Linux offers better tooling and features for software development
- Windows is focued on being more user friendly than developer friendly, windows typically obscures a lot of features and tools a developer would want easy access to
- Bash is a way better shell env than shitty ass Powershellw
- Lots of development tools are developed for either OSX or Linux, Windows support is usually only available if you're lucky.  
- Linux is an industry standard OS for SE, it is worth switching over to and being familiar with.


### What is WSL 2

## Setting Up WSL

### Step 1: Enable WSL

This command will enable the features necessary to run WSL and install the Ubuntu distribution of Linux.

```bash
wsl --install
```

### Step 2: WSL Versioning
With the previous command, you should be set up with WSL 2.

You can check the version with the following command

```
wsl -l -v
```
Switching versions between WSL 1 & 2 is as simple as this command

```bash
wsl --set-version <distro name> <version number>
```
### Step 3: The New Windows Terminal

Windows released a new terminal emulator. It offers syntax highlighting, themes, font customization, transparent backgrounds, a tab bar for multiple shells open at once as well as a management system of all your shell envs/WSL envs 

If you have Windows 11 you should aready have it, if you're still on Windows 10 you can download it from the Microsoft Store

### Step 4: Learning Bash

Hopefully you're pretty familiar with a lot of the basic commands with bash, esp if you have been using GitBash for Windows to emulate a bash env

Such as:

- pwd
- ls -a
- cd
- touch
- cp
- mv




### Step 4: Learning the Linux File System
The first thing you'll notice is youre username and system followed by a tilda, like so:
```
macf@DESKTOP-68IP4FK:~
```


The tilda is the "home" directory, it is sort of the top level directory regarding your account and this env. you can navigate back there by entering 
```
cd 
# or
cd ~
```

However we can go even higher than this, we can navigate to the root to see the system folders

```
cd /
```

Now if you run ls you will see a bunch of folders and even our home directory, cd back into home

You can use the Windows explorer GUI navigate the file system as well

```
explorer.exe .

```

### Step 5: Dot Files

Dot files are basically "secret" files that are publically displayed without a special command

You might be familiar with dot files if you have used .gitignore or .env files

We can reveal all files inclduing our secret ones with

```bash
ls -a
```


### Step 6: Vim & Nano

Linux Distros all come with 2 text editors

Nano: a regualr text-editor, similar to Windows notepad

Vim:  A highly extensible text-editor popular for software development and programming. 


Open vim
```
vim
```
Open nano

```
nano
```

### Step 6: The Advanced Packaging Tool (APT) & apt Command


The apt command is a powerful command-line tool, which works with Ubuntu’s Advanced Packaging Tool (APT). The commands contained within apt provide the means for installing new software packages, upgrading existing software packages, updating the package list index, and even upgrading the entire Ubuntu system.

Some examples of popular uses for the apt utility include:

#### Install a Package

Installation of packages using apt is quite simple. For example, to install the nmap network scanner, type the following:

```
sudo apt install nmap
```
Tip

You can specify multiple packages to be installed or removed, by separating them with spaces.

#### Remove a Package
```
sudo apt remove nmap
```
#### Update the package registry

The APT package index is essentially a database of available packages from the repositories defined in the /etc/apt/sources.list file and in the /etc/apt/sources.list.d directory. To update the local package index with the latest changes made in the repositories, type the following:

```
sudo apt update
```

#### Upgrade packages

Installed packages on your computer may periodically have upgrades available from the package repositories (e.g., security updates). To upgrade your system, first, update your package index with sudo apt update, and then type:

```
sudo apt upgrade
```


__It is advised to always run a registry update and upgrade before installing anything from APT__


### Step 7: Install Some Packages (curl, git, tree, python3, pip, nvm)


Lets set up our new ENV with some software

- curl: a popular command line HTTP request tool
- git: git
- tree: a command line tool for displaying a graphical representation of youre file system
- python3: The Python compiler
- pip: Python package manager

```
sudo apt install curl git tree python3 pip
```

### Step 8: Install the Node Version Manager

The Node Version Manager is a CLI for easily updgrading/downgrading your current node version. Node is constantly updating and versioning is important as certain apps can break because of version clashing. The NVM cli will allow us to install, upgrade, or downgrade our version of node with ease
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```




 


