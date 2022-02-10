# David's Dotfiles

These are a collection of the dotfiles that I use on my personal machine. They include configurations for my window manager (currently Awesome) allong with various other programs that I use day to day.

## Dot file management method

I am using a dotfile management method that was originally popularized on a HackerNews thread, and then formalized in a great write up that can be found [here](https://www.atlassian.com/git/tutorials/dotfiles).

The gist of it is that we create a bare repo in our home directory (I chose ~/.dotfiles), and then create an alias in our .bashrc config to define our working tree as our home directory. This way when we can add any file in the home directory to be version controlled in our bare repository. This keeps everything simple by providing us with version controlled files, while aslo allowing us to add any file in our home directory without needing to do any symlinking to another directory or changing default config file locations.

We then hide all other files that have not been explicitly added to the git repo in order to not have to maintain a gitignore for every file added to the home directory. 

```
git init --bare $HOME/.dotfiles
alias config='/usr/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
dotfiles config --local status.showUntrackedFiles no
echo "alias dotfiles='/usr/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'" >> $HOME/.bashrc
```

We then can use the alias to commit and push files to the repositry. 

e.g. `dotfiles add .bashrc`
  or 
     `dotfiles commit -m "added .bashrc"`
     
## .bashrc

Here are all the custom configurations and aliases in my bash config. Here you will only see the alias created above for dotfile tracking. May add more at a future date!

## Awesome

I am just getting started with AwesomeWm. I love the beautiful setups that can be seen on r/unixporn and the flexibility really applealed to me. This section is going to be incomplete for a while, but work will start!

### Awesome Testing

In order to develop the awesome config files before having a complete working setup, we can create an xserver inside an existing window manager. In this case I have been useing KDE Plasma as my desktop enviroment. We can use Xnest to spwan a window, then run awesomeWm inside that window. 

#### Spawn the Xserver window

`Xnest -ac -geometry 1366x768`

#### Start awesomeWm

`DISPLAY=:1 awesome`
