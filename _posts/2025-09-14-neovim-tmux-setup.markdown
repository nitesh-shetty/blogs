---
layout: post
title:  "Neovim, tmux and plugins"
date:   202 5-09-14 20:38:24 +0530
categories: Linux, neovim, tmux, plugins, workflow 
---

My typical workflow in Ubuntu/Debian involves,  
# Neovim:  
Ubuntu/Debian neovim installation:  
```sudo apt install -y neovim```  

If you are familiar with vi/vim, neovim has similar navigation keymap.  
I would suggest to go through vimtutor, after installation.  
Most of my plugin management comes from [kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim).  
For kernel development, there is extra plugin for vim options.  
Since I use tmux along with neovim, tmux_navigator.lua helps to navigate across multiple tmux panes and vim windows.  

# Tmux:  
Ubuntu/Debian tmux installation:  
```sudo apt install -y tmux```  

If you are working on remote Linux desktop, tmux helps to create multiple session, panes.  
Another advantage is you can keep the session alive even your network connection is lost.  
Effectively, your tmux session is saved until the PC is on.  
I also used tmux resurrect plugin, which restores tmux session.  

> prefix  

To trigger any command related to tmux you need to press a combination of keys,  
called as prefix. This is usally stored in tmux config file, which can be found in  
~/.tmux.conf. My tmux.conf can be found [here](https://github.com/nitesh-shetty/dotfiles/blob/main/tmux.conf)  
```wget https://github.com/nitesh-shetty/dotfiles/blob/main/tmux.conf ~/.tmux.conf```  
Default key mapping for tmux is ctrl+b (press 'control' and 'b' key simultaneously),  
but I changed it to ctrl+a, for convinience. You can change it by editing 'prefix' in  
~/tmux.conf  

# Keymaps:  
## tmux useful keymaps  

Start a tmux session  
```tmux new -s project```  

To detach without, closing the session  
```ctrl+a d```  
here you need to press ctrl and a together, followed by pressing d.  

### tmux panes, windows, sessions:
By default when you open a new session, you get a single pane and single window.  
Then you can create multiple panes inside a single window.  
Mulitple windows create a session.  

A typical scenario where this might happen is.  
Lets say you are working with multiple virtual machines.  
I usually prefet to keep a single window for each VM along with renaming each window.  
In one terminal usually mail is opened. So no need to open multiple session.  
After some time the keymaps will be automatic.  

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
