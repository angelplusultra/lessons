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

WSL 2 is a new version of the Windows Subsystem for Linux architecture that powers the Windows Subsystem for Linux to run ELF64 Linux binaries on Windows. Its primary goals are to increase file system performance, as well as adding full system call compatibility.

This new architecture changes how these Linux binaries interact with Windows and your computer's hardware, but still provides the same user experience as in WSL 1 (the current widely available version).

Individual Linux distributions can be run with either the WSL 1 or WSL 2 architecture. Each distribution can be upgraded or downgraded at any time and you can run WSL 1 and WSL 2 distributions side by side. WSL 2 uses an entirely new architecture that benefits from running a real Linux kernel.

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
- mkdir
- cp
- mv
- sudo
- which
- cat
- echo





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

### Step 5: Dot Files and RC Files

Dot files are  "secret" files/folders that can only be revealed with a special command

They are called dot files because the name of the files/folders are prefixed by a .

Dot files are typicaly related to containing configuration code for a specific program

Some common examples:

- .gitignore
- .bashrc
- .vimrc
- .config

We can pass the "all" flag in our ls command to reveal all files inclduing our secret ones:

```bash
ls -a
```

You should see a file by the name of __.bashrc__, it is an RC File.

RC Files also known as Run Command files ar basically scripts that execute when a program boots. Usually, developers can modify the contents of a RC file to customize the behavior of a program at startup.

Later we'll be coming back to the .bashrc to do some custom scripting.


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

Confirm Installation with

```
nvm -v
```
Install the latest version of node with

```
nvm install latest
```

Confirm installation with

```
node -v

#check npm installation too

npm -v
```

BONUS: Install some global packages with npm, TypeScript compiler and nodemon:

```
npm install -g nodemon typescript
```
### Step 10: A Depper Understanding of Executables, Binaries and the $PATH Variable

As a Windows user, you might be used to the idea that "executables" are simply just files that has a .exe extension, and when you run it, a program executes. in Linux however, anything can be an executable and the .exe extension is a Windows exclusive feature.

Lets make an executable in Linux that will simply just echo "Hello World" in the terminal

```
nano hello
```

In the file, write
```
echo "Hello World"
```

Now with the chmod command we can mark the file as an executable 

```
chmod +x hello
```
The x flag is to set or unset the executable permission of a file. And using + sign before x means we want to set it as an executable file.

This will make the file executable for the owner, group and everyone else. Anyone on the system, will be able to execute it as well.


Now run
```
./hello
```
The file has executed


But notice how if we were to leave the current working directory, that command would no longer execute the file. What if we want it to be globally available like most executables.

For that, we have to understand what the **$PATH Variable** is.


#### $PATH
By default, executing any file that you create or download onto your system requires that you specify the full path to that file. This is a safeguard to prevent you from executing something you don’t intend to execute, because anything that executes on your system has the potential to cause damage if it isn’t used correctly.

It's important to understand at this point, that all your shell commands (ls, mkdir, touch, node, npm, python3, vim) are not working by pure magic, the absolute path to the executable is always needed.

To see where the executables of a command are located

```

which ls

which mkdir

which touch

which node

which npm
```

but here as you can see, we're not specifiying it. It looks like we're simply just calling a command. So what is happening

Any operating system (Windows, MacOS, Linux) uses an environment variable called PATH to determine where executable files reside on your system. An environment variable is just a named value that can be referenced by your operating environment. Developers commonly use environment variables to store information used by their applications, but they are also used by the operating system to store and use configuration.

You can see the PATH set on your system by typing the following in a terminal session:
```
echo $PATH
```
```
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```

the PATH variable is a string of directory paths delimited by a :

Any directory within the string will give global access to any executables within that directory, and can be executed by just entering the file name (e.g node)

So in order for us to make our hello program a global executable, we have to add its directory location to our $PATH variable

But first, we should create a custom folder in our home ~ for any custom executables we want to add to our $PATH and move our hello program into it

**NOTE: IT IS NOT  TO RECOMMENDED JUST ADD YOUR HOME DIRECTORY TO $PATH SO U CAN HAVE ACCESS TO EVERYTHING, IT IS ALWAYS SAFE TO KEEP YOUR PATH DIRECTORIES SEPERATED**

```


mkdir ~/bin/

mv hello ~/bin
```

More on what "bin" is in a minute


Now all we have to do is add our newly created bin folder to our PATH variable

We can do it like so:

```
PATH=$PATH:~/bin
```

Before adding our new directory we concatenate it with the current value of path so we don't override everything in there.

```
echo $PATH
```


Now try running your hello program

```
hello
```

So why did we decide to name the folder /bin. As you might have noticed, there are a few folders in your env called bin/. Bin is short for binary. It refers to a directory that contains executable commands for your application

"Binaries" or "Binary files" are the files which contain compiled source code

So in short, bin/ folders are a convention to store any type of executable file, whether it be compiled binaries themselves or regular executable files.


#### Persiting $PATH

Some distros might expect a /bin folder in the home directory, eliminating the need to do anything else at this point, however if you were to name it anything else like /bin2

Your PATH variable might not persist after your system shuts down

To fix this you need to specify your PATH modifications in your .bashrc file


**RC Files are basically jusrt config files that programs execute at startup**


.bashrc
```
if [ -d ~/bin2 ]
then
    PATH=$PATH:~/bin2
fi
```

The reason why were adding the directory to the path conditionally is because in the case that the directory doesnt exist and bash attempts to add the directory to PATH, bash will throw errors.



### Step 11: Creating Aliases

Aliases are custom single keywords commands that execute full length commands

Lets create an alias called pywatch that will use nodemon to watch changes for a python file we point at and clear the output with each save

```
alias pywatch="nodemon --exec 'clear; python' "
```


Now create a python file and write a console log

```
print("yuh")
```

Execute our new alias by pointing it at the file 

```
pywatch index.py
```

Our alias works but it will be lost the minute our shell closes, to have our aliases persist we need to add them to our .bashrc file

Our .bashrc is already expecting a .bash_aliases file, so lets create that for all our custom aliases

.bash_aliases
```
alias pywatch="nodemon --exec 'clear; python' "
```
### Step 12: VSCode WSL Integration

You can set up your Windows installation of VSCode to link with your WSL environments and develop within them


9.1 Install the WSL plugin from the VSCode plugin marketplace 


Try running
```
code .
```

You might be asked to install wget to download the vscode server, Wget is a command-line tool that makes it possible to download files and interact with REST APIs. if so:

```
sudo apt install wget
```

### Step 13: Zsh & Oh-My-Zsh

Zshell works almost identically to the standard BASH shell found on default Linux installs. What makes it different is its support for plugins and themes, along with some extra features like spelling correction, syntax-highlighting, autocompletion, and recursive path expansion


Besides plugin support,zsh features a lot of QOL improvements for working within a shell, such as:

- Automatic cd: Just type the name of the directory
- Recursive path expansion: For example “/u/lo/b” expands to “/usr/local/bin”
- Spelling correction and approximate completion: If you make a minor mistake typing a directory name, ZSH will fix it for you

10.1 Install zsh

```
sudo apt install zsh
```
 Select 0

 10.2 Install OhMyZsh

 ```
 sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
 ```

 OhMyZsh comes bundles with countless plugins and themes which just have to be enabled in the newly created .zshrc file in your home directory, you can browse the lot here

 https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins

 https://github.com/ohmyzsh/ohmyzsh/wiki/Themes



Lets enable a few OhMyZsh plugins and select a theme



.zshrc
```
ZSH_THEME="random"
plugins=(git node" jump web-search themes)
```
 10.3 Install auto-suggestions plugin and syntax-highlighting


 ```
# AS
 git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# SH
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
 ```
Add them to to your plugins
```
plugins=(git node" jump web-search themes auto-suggestions syntax-highlighting)

**If you really wanna go crazy with a sexy looking terminal you can look into the Powerlevel10k theme for zsh**
```




## Conclusion

You're a 10x dev now mf

You can continue configruing and extending your WSL environment with apps and plugins
