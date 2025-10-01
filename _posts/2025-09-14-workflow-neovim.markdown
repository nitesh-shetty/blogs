---
layout: post
title:  "Workflow, Neovim, tmux and plugins"
date:   2025-09-14 20:00:00 +0530
categories: linux workflow neovim tmux plugins
---

My typical workflow in Ubuntu/Debian involves,  
Neovim as editor, Tmux for window/session management.  

# TL,DR  
I usually put things inside scripts, instead of setting up tools and configs everytime,  
Below steps should help you to setup neovim and tmux and use the keymap to get started.  
```git clone https://github.com/nitesh-shetty/helper_scripts.git```  
```cd helper_scripts/ubuntu```  
```chmod a+x ./setup.sh```  
```./setup.sh nvim```  
```./setup.sh tmux```  

## Keymaps  
## neovim useful keymaps
To see all the currently opened file,  
```space+space```  

To search files,  
```space s f```  
you need to press space, first followed by s, followed by f  

To grep a string,  
```space s g```  

## tmux useful keymaps  
 
Start a tmux session  
```tmux new -s project```  

To detach without, closing the session  
```ctrl+a d```  
here you need to press ctrl and a together, followed by pressing d.  

### tmux panes, windows, sessions:
By default when you open a new session, you get a single pane and single window.  
Then you can create multiple panes inside a single window.  
Multiple windows create a session.  

A typical scenario where this might happen is.  
Lets say you are working with multiple virtual machines.  
I usually prefer to keep a single window for each VM along with renaming each window.  
In one terminal usually mail is opened. So no need to open multiple session.  

#### Creating multiple panes:  
Splitting the window and creating panes,  
I felt | and - are intuitive of vertical and horizontal split respectively.  
Hence,  
To vertically split the window,  
```ctrl+a shift+\```  
or  
```ctrl+a |```  

To horizontally split the window,  
```ctrl+a shift+-```  
or  
```ctrl+a _```  

You can check in ~/tmux.conf and change the keymap to your convience,  
just check for split-window.  

Since panes are smaller and you want to full-screen the pane you are working on.  
```ctrl+a z```  

Since I also integrated tmux-navigator and premmaped tmux keys mapping ~/.tmux.conf,  
below should be useful to move between panes.  

Move 'up' to pane above:  
```ctrl k```  

Move 'down' to pane below:  
```ctrl j```  

Move 'left' to pane:  
```ctrl h```  

Move 'right' to pane:  
```ctrl l```  

#### Creating multiple windows:  
To create a new window  
```ctrl+a c```  

To rename a window  
```ctrl+a ,```  

To move to next window  
```ctrl+a n```  

To move to previous window  
```ctrl+a p```  

To move to 2nd window  
```ctrl+a 2```  
Similarly you can replace 2 to any nth window.  


#### Resizing the panes:  
To expand the current pane up:  
```ctrl+a k```  

To expand the current pane down:  
```ctrl+a j```  

To expand the current pane left:  
```ctrl+a h```  

To expand the current pane right:  
```ctrl+a l```  

# Long read
To know about how helper_script setups the neovim and tmux,  
# Neovim:  
Ubuntu/Debian neovim installation:  
```sudo apt install -y neovim```  

If you are familiar with vi/vim, neovim has similar navigation keymap.  
I would suggest to go through vimtutor, after installation.  
Most of my plugin management comes from [kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim).  
For kernel development, there is extra plugin for vim options.  
Since I use tmux along with neovim, tmux_navigator.lua helps to
navigate across multiple tmux panes and vim windows.  

Configuring kickstart.nvim,  
```git clone https://github.com/nvim-lua/kickstart.nvim.git ~/.config/nvim```

### plugins:  
*vim_options*:  
This is my customization carried from previous my previous vim legacy.  
Some of the key bindings are related to Linux kernel developement such as,  
getting to know we should wrap around at column 80.  
Configuration:  
```wget https://github.com/nitesh-shetty/dotfiles/blob/main/vim_options.lua ~/.config/nvim/lua/custom/plugins/vim_options.lua```  

*tmux_navigator.lua*:  
This plugin helps to navigate from neovim to other terminal when using inside tmux.  
Configuration:  
```wget https://github.com/nitesh-shetty/dotfiles/blob/main/tmux_navigator.lua ~/.config/nvim/lua/custom/plugins/tmux_navigator.lua```  

*vimtex.lua*:
This plugin is realted to latex, here we configure vimtex view method as zathura.  
If you not using latex, you can skip this step.  
Configuration:  
```wget https://github.com/nitesh-shetty/dotfiles/blob/main/vimtex.lua ~/.config/nvim/lua/custom/plugins/vimtex.lua```  

Lets say, you are inside neovim editor and want to move to right side pane then press,  
```ctrl + l``` 
similarly other keys,  
```ctrl + h``` for moving to left pane  
```ctrl + j``` for moving to down pane  
```ctrl + k``` for moving to up pane  
```ctrl + l``` for moving to right pane  

> leaderkey  or mapleaderkey or prefix

To trigger any command related to neovim you need to press a combination of keys,  
called as mapleaderkey.
This is usually stored in neovim config file, which can be found in ~/.config/nvim/init.lua.  
My leaderkey is default 'space key'. My init file is [here](https://github.com/nvim-lua/kickstart.nvim/blob/master/init.lua)  
You can change it by editing 'vim.g.mapleaderkey' in  ~/.config/nvim/init.lua   

# Tmux:  
Ubuntu/Debian tmux installation:  
```sudo apt install -y tmux```  

If you are working on remote Linux desktop, tmux helps to create multiple session, panes.  
Another advantage is you can keep the session alive even your network connection is lost.  
Effectively, your tmux session is saved until the PC is on.  

> prefix  

To trigger any command related to tmux you need to press a combination of keys,  
called as prefix.
This is usually stored in tmux config file, which can be found in  
~/.tmux.conf. My tmux.conf can be found [here](https://github.com/nitesh-shetty/dotfiles/blob/main/tmux.conf)  
```wget https://github.com/nitesh-shetty/dotfiles/blob/main/tmux.conf ~/.tmux.conf```  
Default key mapping for tmux is ctrl+b (press 'control' and 'b' key simultaneously),  
but I changed it to ctrl+a, for convenience.
You can change it by editing 'prefix' in  
~/tmux.conf  

#### tmux plugins:
Tmux comes with plugin management, such as [tpm](https://github.com/tmux-plugins/tpm).  
```git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm```

*tmux-continuum*: this plugin saves the tmux sessions every 15 minutes  
*tmux-resurrect*: this plugin helps to recover the previously saved session
from tmux-continuum  
*tmux-themepack*: jimeh/tmux-themepack gives a clean elegant look to tmux session  
Add below lines to ~/.tmux.conf if you want to integrate the above plugins.  
set -g @plugin 'tmux-plugins/tpm'  
set -g @plugin 'jimeh/tmux-themepack'  
set -g @plugin 'tmux-plugins/tmux-resurrect'  
set -g @plugin 'tmux-plugins/tmux-continuum'  
set -g @themepack 'powerline/default/yellow'  
set -g @resurrect-capture-pane-contents 'on'  
set -g @continuum-restore 'on'  
run '~/.tmux/plugiins/tpm/tpm'  

After adding above lines in ~/.tmux.conf, to install plugins  
```ctrl+a shift+i```

