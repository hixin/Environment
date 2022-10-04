### zsh 安装
https://itslinuxfoss.com/how-to-install-zsh-in-ubuntu-22-04/#:~:text=To%20install%20Zsh%20in%20Ubuntu%2022.04%2C%20open%20the,the%20installation%20method%20of%20Zsh%20on%20Ubuntu%2022.04.


Step 1(Optional): Locate the Zsh Utility

```$ apt show zsh```


Step 2: Install Zsh

```$ sudo apt install zsh -y```

Step 3: Install Configuration Tool of Zsh

```$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"```


Step 4: Test Zsh Shell

```$ sudo apt update```

To find out the zsh shell directory, run the command:

```which zsh```

To switch the bash shell from the zsh shell, use the command:

```exec bash```

To change theme

```omz theme set agnoster```

Similarly, the “exec zsh” will switch the shell from bash to zsh.

Step 5: Configure your zsh

The default plugin is git, you can add you plugin as you like:

git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions


git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
vim ~/.zshrc

plugins=(
git z zsh-autosuggestions extract web-search zsh-syntax-highlighting
)
```
After add plugin, you just need do

```omz reload```




-----
Removing Zsh From Ubuntu 22.04

If you want to remove the zsh utility from Ubuntu 22.04, use the below-stated command:

```$ sudo apt purge zsh -y```


### qemu 安装
https://www.cnblogs.com/binarysystemloophole/p/15703394.html


```sudo apt install qemu```


