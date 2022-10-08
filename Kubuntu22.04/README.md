## 系统安装
https://blog.csdn.net/weixin_44410537/article/details/110672115


Step1:
选择默认的LVM安装，最小安装

默认的LVM根文件系统会使用整个磁盘,安装完成后，拔掉U盘，正常启动，到了登录页面直接关机。

Step2：插上U盘重启进入U盘试用系统

因为缩容需要卸载根分区，所以需要在u盘系统上进行,终端执行lsblk，可以看到创建VG vgkubuntu，并创建了两个lv root和swap_1

缩容操作不建议使用lvreduce，对原理不熟悉的话很容易导致无法开机，建议直接使用无损工具

```
# 扩充比较容易 /dev/mapper/vgkubuntu-root 和 /dev/vgkubuntu/root 是一回事
# sudo lvextend -L +4G /dev/mapper/vgkubuntu-root
```


Step3：关机拔掉U盘，重启进入安装系统

创建逻辑分区home, 将来挂在home

lvcreate -l +90%FREE -n home vgkubuntu
mkfs -t ext4 /dev/mapper/vgkubuntu-home

## 软件安装

### terminator 安装

号称ubuntu下最好用的终端

```sudo apt install terminator```

### flameshot 安装

号称ubuntu下最好用的截图工具

``` sudo apt install flameshot```

### peazip 安装

号称ubuntu下最好用的压缩工具

```
sudo apt install ./peazip_8.8.0.LINUX.Qt5-1_amd64.deb
```

### anyconnect安装

翻墙工具，需要账号，先解压
anyconnect-linux64-4.10.01075-predeploy-k9.tar.gz
```
cd anyconnect-linux64-4.10.01075/vpn
sudo env LAUGUAGE=en ./vpn_install.sh
```

### chrome安装

```
sudo apt install ./google-chrome-stable_current_amd64.deb
```
### 号称ubuntu最好用的查找软件

https://github.com/cboxdoerfer/fsearch

```
sudo add-apt-repository ppa:christian-boxdoerfer/fsearch-stable
sudo apt update
sudo apt install fsearch
```
### wps安装
```
sudo apt install ./wps-office_11.1.0.11664.XA_amd64.deb

若无法运行可参考

https://blog.csdn.net/Steven_Start/article/details/124566000?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-124566000-blog-124387876.t0_edu_mix&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-124566000-blog-124387876.t0_edu_mix&utm_relevant_index=1
```

### vscode安装

```
sudo apt install ./code_1.70.1-1660113095_amd64.deb
```
插件登录github账号即可同步

### 钉钉安装

直接官网下载就好
```
sudo apt install ./com.alibabainc.dingtalk_1.4.0.20829_amd64.deb
```
### 微信安装

优麒麟商店下载

```
sudo apt install ./weixin_2.1.1_amd64.deb
```

### 飞书安装

直接官网下载最新就好
```
sudo apt install ./Feishu-linux_x64-5.14.14.deb
```

### xmind安装
```
sudo apt install ./Xmind-for-Linux-amd64bit-22.09.3169.deb
```

### 百度网盘安装

```
sudo apt install ./baidunetdisk_4.14.5_amd64.deb
```

### 网易云音乐安装

```
sudo apt install ./netease-cloud-music_1.2.1_amd64_ubuntu_20190428.deb
```
22.04 闪退

/opt/netease/netease-cloud-music/netease-cloud-music.bash 倒数第二行添加cd /lib/x86_64-linux-gnu/

```
#!/bin/sh
HERE="$(dirname "$(readlink -f "${0}")")"
export LD_LIBRARY_PATH="${HERE}"/libs
export QT_PLUGIN_PATH="${HERE}"/plugins
export QT_QPA_PLATFORM_PLUGIN_PATH="${HERE}"/plugins/platforms
cd /lib/x86_64-linux-gnu/
exec "${HERE}"/netease-cloud-music $@

```

### finalShell 安装

ubuntu缺乏类似xshell的工具,这个工具功能完美，只不过是java实现的，资源占用高，UI有点low

finalshell_install_linux 脚本会去下载
http://dl.hostbuf.com/finalshell2/finalshell_linux.zip?v=23579


```
一键安装脚本
rm -f finalshell_install_linux.sh ;wget www.hostbuf.com/downloads/finalshell_install_linux.sh;chmod +x finalshell_install_linux.sh;./finalshell_install_linux.sh;

安装路径
/usr/lib/FinalShell/
配置文件路径
/home/$USER/.finalshell/

卸载
删除安装目录 /usr/lib/FinalShell/

```
### vm player安装

```
第一步是安装构建依赖项。打开终端并运行以下命令：
sudo apt update sudo apt install build-essential linux-headers-generic

最新版本的VMware Workstation Player可以从VMware 下载页面下载
https://customerconnect.vmware.com/en/downloads/details?downloadGroup=WKST-PLAYER-1624&productId=1039&rPId=91446

chmod a+x VMware-Player-Full-16.2.4-20089737.x86_64.bundle

sudo ./VMware-Player-Full-16.2.4-20089737.x86_64.bundle  --required --eulas-agreed
```

### audacity 安装
官网都是appimage 格式了，好是好，没有图标啦
直接Discover下载安装了

### easyconnect 安装
公司vpn工具
```
sudo apt install ./EasyConnect_x64_7_6_7_3.deb

22.04 无法启动

sain@Linux  /usr/share/sangfor/EasyConnect  ldd EasyConnect | grep pango
        libpangocairo-1.0.so.0 => /lib/x86_64-linux-gnu/libpangocairo-1.0.so.0 (0x00007fb59079f000)
        libpango-1.0.so.0 => /lib/x86_64-linux-gnu/libpango-1.0.so.0 (0x00007fb5905e0000)
        libpangoft2-1.0.so.0 => /lib/x86_64-linux-gnu/libpangoft2-1.0.so.0 (0x00007fb58ed0b000)
 sain@Linux  /usr/share/sangfor/EasyConnect 

 解决方案：
 安装目录上放三个之前版本的so，避免使用系统目录的so

 sudo cp easyconnectpatch/* /usr/share/sangfor/EasyConnect/
```

### 投屏软件vysor

(echo 'deb [arch=amd64, trusted=yes] https://nuts.vysor.io/apt ./' | sudo tee /etc/apt/sources.list.d/vysor.list) && sudo apt update && sudo apt install vysor

### ripgrep安装
```
RIPGREP_VERSION=$(curl -s "https://api.github.com/repos/BurntSushi/ripgrep/releases/latest" | grep -Po '"tag_name": "\K[0-9.]+')

curl -Lo ripgrep.deb "https://github.com/BurntSushi/ripgrep/releases/latest/download/ripgrep_${RIPGREP_VERSION}_amd64.deb"

sudo apt install -y ./ripgrep.deb
```


### docker 安装和环境搭建
https://zhuanlan.zhihu.com/p/344082401

https://docs.docker.com/engine/install/ubuntu/#set-up-the-repository
```
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?

```
systemctl start docker
systemctl status docker
```

Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/json": dial unix /var/run/docker.sock: connect: permission denied
```
sudo usermod -aG docker $USER
newgrp docker
systemctl restart docker
# 或者service docker restart

```
```
docker pull ultraji/ubuntu-xfce-novnc

```
### multipass安装
https://multipass.run/install
装上22.04 有些编译就遍不过了,是和libc.so有关系,不是很好解决. 保留一套18.04 的环境

Step1: 创建dev虚拟机
multipass launch 18.04 -n dev -c 4 -m 4G -d 6G


Step2: 目录映射
multipass mount /home/sain/work/01code dev:/home/ubuntu/01code

Step3: 进入虚拟机
multipass shell dev



### 安装ssh，vim
sudo apt install vim
sudo apt install openssh-server
sudo systemctl start ssh
sudo systemctl status ssh

### zsh 安装
https://itslinuxfoss.com/how-to-install-zsh-in-ubuntu-22-04/#:~:text=To%20install%20Zsh%20in%20Ubuntu%2022.04%2C%20open%20the,the%20installation%20method%20of%20Zsh%20on%20Ubuntu%2022.04.


Step 1(Optional): Locate the Zsh Utility

```$ apt show zsh```


Step 2: Install Zsh

```$ sudo apt install zsh -y```

Step 3: Install Configuration Tool of Zsh

sudo apt install curl

```$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"```

国内网基本不行, 直接复制执行
```
sh -c "$(curl -fsSL https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh \
    | sed 's|^REPO=.*|REPO=${REPO:-mirrors/oh-my-zsh}|g' \
    | sed 's|^REMOTE=.*|REMOTE=${REMOTE:-https://gitee.com/${REPO}.git}|g')"
```

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
git z zsh-autosuggestions extract web-search zsh-syntax-highlighting sudo
)
```
After add plugin, you just need do

```omz reload```




-----
Removing Zsh From Ubuntu 22.04

If you want to remove the zsh utility from Ubuntu 22.04, use the below-stated command:

```$ sudo apt purge zsh -y```


### qemu 安装
主要是为了搭建linux 0.12 环境
https://www.cnblogs.com/binarysystemloophole/p/15703394.html

后面参考bochs方案，qemu暂时不需要，后续用到再补充

https://www.qemu.org/docs/master/system/index.html

Ubuntu18.10开始qemu是一个空包，应该安装qemu-system-x86

```sudo apt install qemu-system-x86```



## 配置调整

Step1： 关键目录添加保护

这次重装系统，就是不小心把etc目录全部删除了，尽管后面想各种方式恢复了，但系统总感觉不对劲
特别是背光调节，怎么都回不去

----背景知识-----
https://blog.csdn.net/codedancing/article/details/103835085
https://www.runoob.com/linux/linux-comm-chattr.html

i：不得任意更动文件或目录, 即文件只读
a：让文件或目录仅供附加用途。

sudo chattr -V +a test
默认只会给当前目录加属性， 当前子目录不能删除，子目录内的还是能被删除的

-R：作用于目录时，会显示所有的子目录和文件的隐藏信息
lsattr -R test

加了-V 会打印日志：
chattr: Operation not supported while reading flags on /etc/systemd/system/paths.target.wants/acpid.path

The error was due to the file I was trying to chattr being a symlink, not a real file
----背景知识-----

保护关键目录etc：
加锁
sudo chattr -RV +a /etc
取消加锁
sudo chattr -RV -a /etc


Step2： 特殊按键映射（mac机器可能用到）

由于自己经常用mac，习惯了cmd用作ctrl，切换到ubuntu上，经常错按
希望修改按键映射，达到目地如下：
1. 左cmd和ctrl一样
2. 由cmd和win功能一样

 sain@Linux  ~  setxkbmap -print
xkb_keymap {
	xkb_keycodes  { include "evdev+aliases(qwerty)"	};
	xkb_types     { include "complete+numpad(mac)"	};
	xkb_compat    { include "complete"	};
	xkb_symbols   { include "pc+macintosh_vndr/us+inet(evdev)+altwin(ctrl_win)"	};
	xkb_geometry  { include "macintosh(macbook78)"	};
};


修改 /usr/share/X11/xkb/symbols/altwin



## 数据备份

### 快照备份

https://www.learndiary.com/2021/11/snapshot-of-lvm/

没有安装软件，完成基本分区
sudo lvcreate -s -L 16000M -n rootsnap20221006 /dev/mapper/vgkubuntu-root -v

安装完全部软件(包括AndroidStudio，配置完全调整好)
sudo lvcreate -s -L 18000M -n rootsnap20221007_allapp /dev/mapper/vgkubuntu-root -v

### 物理备份

ubunut 每次装完，配置环境，装软件很麻烦。把和软件相关的目录全都备份一下

Step 1：etc opt snap usr 目录使用tar打包

tar: etc/security/opasswd: Cannot open: Permission denied
需要root权限才可以， tar -cpvf

```
cd /
su
tar -cvpf /home/sain/etc_opt_snap_usr.tar etc opt snap usr
```


Step 2：新建home_backup 目录， 将home目录下所有隐藏文件拷贝一份， 然后使用tar打包

先要清空回收站
~/.local/share/Trash
```


mkdir home_back
cd
cp -a -r .* home_back/
# du -sh .* | sort -rh (复制完，可以先看下各目录大小，避免备份回收站)
tar -cvf home_backup.tar home_backup
```

Step3： 其它备份

其他home目录的备份，可以自己用tar包的方式

### 恢复

Step1：

etc_opt_snap_usr.tar 用于覆盖etc opt snap usr目录
tar -xvpf（解压命令要加p）

恢复的时候,记得目标机的/etc/fstab 要保留, 一般不能直接覆盖


Step2：
home_backup.tar 用于覆盖用户目录下的隐藏文件


