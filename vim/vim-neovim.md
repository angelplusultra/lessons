# The Ultimate Vim + Neovim Course By Rakk


## Vi, Vim, Neovim?
 
### Vi

Vi is one of the first text-editors ever invented. It was created in 1976 and is still somehow being used today by some people


### Vim 

Vim is a Unix text editor that's included in Linux, BSD, and macOS. It's known for being fast and efficient, in part because it's a small application that can run in a terminal (although it also has a graphical interface), but mostly because it can be controlled entirely with the keyboard with no need for menus or a mouse. For instance, to insert text into a file, you press I and type. To navigate or to issue a command (such as Save, Backspace, Home, End, and so on), you press Esc on your keyboard and then press whatever key or key combination corresponds with the action you want to take. It's a very different way of editing text compared to what modern computer users expect, but it's the way Unix admins all over the world edit config files, changelogs, scripts, and more.

Vim is also commonly referred to as Vi because when it was written by Bill Joy in the late 1970s, it was short for visual editor. Before Vi, few people even imagined that a computer could act as a sort of interactive typewriter. Text files were edited with commands (like ed) that would find a specific line and either insert or remove text; literally all text was manipulated with what amounted to a rudimentary version of your favorite office application's find-and-replace menu (but without the office application). Vi was a breath of fresh air, enabling users to enter a screen session that showed them their entire file and allowed them to edit it live.
### Neovim

Neovim is a fork of Vim that was released in 2015. While Neovim is still up and coming, The Vim community has been migrating over to Neovim for its improvements upon base Vim as well as featuring Lua as it's embedded scripting language as opposed to VimScript, which is widely despised by the Vim Community.
If you ask me, Neovim is the best way to be a Vimbecile in 2023, and when we get to actually building our own Vim text-editor, we're gonna be using Neovim instead.

## What Makes Vim Different than Other Text-Editors?

### The Vim philosophy is basically to equip you with everything you could possibly need to do with just your keyboard and reduce mouse usage to an absolute minimum

Vim has a very opinionated and robust key system that is unlike any other text-editor software you have eveer touched in your life

Because of this, Vim is known to have a learning curve, but matsering the vim key system is proven to pay off in terms of improving your speed and efficiency while coding 

Vim is not an IDE. Vim out-of-the-box does not contain many features you might be used to having in many "plug-n-play" text-editors like VsCode 

Features like

- Syntax Highlighting
- Language Support
- Auto-Completion
- File Tree
- GUI extensions (tabline, status bar)

All have to be to be configured manually with embedded scripting

However that doesnt mean in order to get Vim to be an IDE like VsCode it will require you to basically code VsCode from scratch.

Vim has a pasisonate plug-in ecosystem and community where many features are simply an act of drag and drop.








## Why the Fuck Should I Use a Text-Editor That's 30 years old?

I like to think of Vim as two seperate things. 

- Vim: The Key System
- Vim: The Text Editor

Let's start with the first one:

### Why the Fuck should I learn the Vim Key System

The Vim Key System is alone one of the best benefits of picking up Vim. The key system is designed for your hands to stay around the home row and increase your typing speed.
If your not particularly a hot key junky, you'll immediately see improvements to your productivity when using Vim. Something as simple s highlighting and deleting a block of code will be executed faster and feel better to do than the standard mouse technique

The Vim Key System is so beloved that even if you have no interest in using vim as a text-editor, every single modern IDE features some sort of Vim mode or plug-in that will emulate its key-system within that text-editor environment

Even Leetcode and Codewars features the option to enable Vim

### Why the fuck should I use the Vim Text-Editor?
Well...Vim is highly-extensible and gives you basically the complete freedom to customize and modularize it however you want.

Honestly...Besides the benefits of using "real" vim as opposed to some plug-in emulator in a modern IDE.
Unless youre geneuinely interested in how an IDE really works under the hood and care about having that freedom to modularize your text-editor in whichever way you want. Vim as an editor experience might not be for you.

That being said, learning how to build my own vim configs has taught me an insane amount about IDE development and everytime I go back to VsCode im shocked by how many features I can count that I dont have out of the box in Vim.

However, if the "build your own vim cofnig from scratch" schtick doesn't sound like your thing, there's countless popular pre-builds you can find online that basically give you a VsCode in Vim experience with little to no extra configuration





## Learn to Vim
We're gonna begin our Vim journey with just plain ol Vim and get going with the basics there. Later we'll take a look at the Vim plugin for Vscode and when we're ready to build our own Vim IDE we'll make a full switch to Neovim


Open Vim
```
vi
```

The core of Vims functionality is surrounded by 4 "modes"

- Normal Mode: Used mainly for code navigation + copying/pasting/deleting
- Insert Mode: Used for editing the buffer
- Visual Mode: Highlighting/Selecting text
- Command Mode: Used for calling "commands" eg(save file, quit, open terminal)

Right now we are in Normal Mode, and as you can probably tell, you can make any edits to the file. Lets not worry about that for now, right now lets learn about Normal Mode

Normal Mode is primarilly used for file navigation, copying/pasting, line deletion


### The Basics

#### Basic Navigation:

- j - Down
- k - Up
- l - Right
- h - Left


You might have noticed that you can also navigate with the arrows keys however it is not recommended to navigate that as it removes your hand away from the home row aka not the real vim way

#### Vertical Navigation:

```
- <S-{> - Leap up a block
- <S-}> - Leap down a block
- G - Bottom of Buffer
- gg - Top of Buffer
- <C-u> - Leap half up the buffer
- <C-d> - Leap half down the buffer
```

#### Horizontal Navigation:

```vim
 w - Leap to the beginning of the next word
 e - Leap to the end of the next word
 b - Leap to the beginning of the previous word
 ge -Leap to the end of the of the previous word
 $ - End of Line
 0 - Beginning of Line

```

### Insert Mode

Alright I'd say its about time to learn a different mode

Insert mode is the mode used for any buffer editing

Theres a few ways to get into insert mode, lets go over the main ones.

```
i - Insert
o - Enter insert mode down a line
a - Enter insert mode next to the cursor (append)

```
Now you can write to the buffer freely, however you ntoice how none of our normal mode keys arent working. We have to return to normal mode

There really isnt much to insert mode as all of the keys are just reserved to be what theyre displayed to be and and printed to the buffer

```
<esc> - Normal Mode
<C-{> - Normal Mode
```





### Find & To
Find and To are ways to navigate to a character After or Before the placement of the cursor

Find brings the cursor the location of the character
To bring the cursor right before the location of the character
```
## After Cursor
fG
tm

## Before Cursor

Fg
Tm



```

### Yank/Paste

```
yy - yank entire line
Y yank to end of line
p - paste be                                                      
P - past ebfore cursor
```


### Delete
```
dd - Delete entire line
D - Delete to end of line

```

### Change

```
cc - change deletes content and changes to insert mode
C - change to end of line

```

### Undo/Redo

```
u - undo
<C-r> - redo
```
### Remove Character

```
x
```


### Hit Da Combos
We can combinate keys for filthy combos

```
dw - Delete Word
cw - Change Word
cfP - Change till we find P
```


### Inner & Around

Inner and Around are two special keys that are mainly used in combination with others

```
ciw - Change Inner Word
ci) - Chane Inner )
di" - Delete Inner "
ya' - yank around '

```

## Visual Mode

Visual Mode is used to highlight and select text so you can make revisions or yank in bulk

```
v - visual line
V - visual block
```
Try highlighting a block of text and hit d, c, y to see the results


## Command Mode

Alright i think we ready for command mode

Command mode is used to perform all sorts of different commands given to you by the editor + plugins

We'll also use command mode later to do some searching


At this point im sure these 4 questions have been in your head

1. How do we save the file
2. How do we quit vim
3. Why aren't there any numbers?

To do both of these things we need to enter command mode

: will enter command mode, if you press <TAB> you will see a bar of completion suggestions, as you can see theres a shit ton of fucking commands

To save the file all we need to enter is




```
:w 
```

To quit the file

```
:q
```

We can combo these together like this

```
:wq
```
To force quit aka quit without saving

```
:q!
```

Now lets enable line numbers
```
:set number
```

and relative numbers
```
:set rnu
```
Lets see some other commands

Vim comes with a handful of built-in shitty color themes, lets enable one now!


```
:colorscheme 
```



Lets open a terminal buffer to the right
```

:rightb vert term
```


## Searching

```
/ ##type character patter
```
When you hit enter all matching patterns will be highlighted, we can jump between them with

```
n - next
N - previous 
```

Oh no it looks like some emacs users have corrupted my file with a bunch of vim hate-speech

We need to change every instance of the word "Vim" into emacs

<br />

<br />

vim is for fags and emacs rules

vim is for fags and emacs rules

vim is for fags and emacs rules

vim is for fags and emacs rules

<br />

<br />
One way to do this by searching
```
/emacs
```
Hit enter and your cursor should be over th first match

Type
```
cgn ## change matching pattern
```
and enter vim and return to normal mode

```
. ## to rpeeat previous action
```
Another way to accomplish this is hit
```
*
```

over any word pattern you want to match for


However while the confim selection approach can be usseful at times, its not appropriate here as we are certain we want to change every instance of emacs within this block and smashing the period button is cumbersome

In visual mode, let's highlight the code block and hit :
<br />

<br />

vim is for fags and emacs rules

vim is for fags and emacs rules

vim is for fags and emacs rules

vim is for fags and emacs rules

<br />

<br />

```
:s/emacs/vim/g
```


There u go playboi show them bitch ass emacs users wasg


## Using Vim in VsCode

Pretty much every modern IDE has some sort of Vim mode or Vim plug-in available in their marketplace. I would say in order to practice Vim until we have our Neovim build, you should use the Vim plugin.
That way you'll have all of the desired features of a modern IDE and the vim key system at your disposal, so you can actually USE Vim as opposed to just dicking around with it. I highly suggest that at this point you just start using Vim for everything you do



## Neovim


At this point, the Vim Key System should be well understood and we can start working on learning Vim as a text-editor. However, we're not gonna learn Vim (the text-editor) per-se, but its newer succesor Neovim.

### Why? 

As far as the decision for the text-editor goes, most people are mvoing over to Neovim. On top of just generally improving base Vim features, Neovim completely overhauled Vim's embedded scripting engine and replaced it with Lua.

Vim had a lot of issues previously with scripting because it only allowed scrpting with it's own utility language VimScript. Which is complete utter ass and nobody likes. Lua on the other hand, is an actual language that people use and actually resembles some sort of programming language like python or javascript.

Besides that as far as modern Vim usage and development is concerned, all of the cool new features and plugins are going to be made for Neovim at this point.

So thats why we're going to build our text-editor with Neovim over Vim



### Installation

```
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim.appimage
chmod u+x nvim.appimage
./nvim.appimage
```
If the appimage command fails
```
./nvim.appimage --appimage-extract
./squashfs-root/AppRun --version

# Optional: exposing nvim globally.
sudo mv squashfs-root /
sudo ln -s /squashfs-root/AppRun /usr/bin/nvim
nvim
```


The command nvim should open Neovim globally
```
nvim
```


As you can see, it's not much different than Vim, we have a lot of configuration to do.



### .config & an Intro to Lua

Neovim is expecting all of its config scripting to be inside of dot folder in the home directory called .config


```
mkdir ~/.config/nvim
```
