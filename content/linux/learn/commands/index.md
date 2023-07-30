---

title: "Linux 常用命令"
date: 2023-07-22T16:29:21+08:00
draft: False
tags: ["Commands"]

---
Linux 常用的命令及相关的基础知识

## 1.Linux 常用指令

```Bash
安装
sudo dpkg -i package_name.deb
复制
sudo cp -r ~/下载/jbr jbr
删除
sudo rm -r Goland-2023.1.2/
查看进程并过滤所需的端口
netstat -anp | grep 5678
查看
lsof -i：5678
删除
kill -9 174189

goland 安装
sudo tar -C /usr/local -xzf  goland-2020.3.4.tar.gz

hostname
hostname -I

df 查看当前系统中挂载的文件系统类型、各文件系统 inode 使用情况及文件系统挂载点
df -i --print-type

ctrl + h // 查看隐藏文件

// 使用该 file 实用程序指示行结尾的类型
file testfile.txt
```

找出文本行尾符： https://stackoverflow.com/questions/3569997/how-to-find-out-line-endings-in-a-text-file

## 2.vim 学习及指令

vim一共分为三种模式，分别为：命令模式，输入模式，退出模式。

启动vim，进入命令模式，在这样的状态下输入任何东西都会被vim识别为命令，比如我们输入i，并不是输入的是字符而是i这个命令。那么“i” 就是常用的命令，他表示切换到输入模式，只有进入到输入模式才能输入字符。

* 命令模式：`:`表示切换到命令模式，在最后一行输入命令
* 输入模式：进入到vim中，按下`i`命令，进入输入模式，在输入模式中可以使用以下指令
* 退出模式：在输入完之后想保存退出，那么就要用到以下
	* `q`：表示退出，没有做过任何编辑
	* `wq`：编辑完之后，保存并退出
	* `q!`：强制退出，放弃修改
	* `wq!`：强制退出并保存（对自己的文件或者root用户）


## 3.Linux 程序安装

### 3.1 deb 安装

```Bash
sudo dpkg -i package_name.deb
```

### 3.2 AppImage 安装

```
// 在 /opt/ 创建程序文件夹
sudo mkdir /opt/obsidian

// 将下载的 AppImage 文件移动至该文件下
sudo mv ~/Downloads/Obsidian-0.12.19.AppImage /opt/obsidian/Obsidian-0.12.19.AppImage

// 赋予执行权限
chmod 777 /opt/obsidian/Obsidian-0.12.19.AppImage

// 在 /bin/ 文件下做一个链接
sudo ln -s /opt/obsidian/Obsidian-0.12.19.AppImage /bin/

// 加入启动器
sudo vi /usr/share/applications/obsidian.desktop

// 编辑内容
[Desktop Entry]
Encoding=UTF-8
Name=Obsidian
Exec=/opt/obsidian/Obsidian-0.12.19.AppImage
Icon=/opt/obsidian/Obsidian.png
Terminal=False
Type=Application
StartupNotify=False
Categories=Application;Development

// 好像也有简版
[Desktop Entry]
Name=obsidian
Exec=/opt/Obsidian-1.3.5-arm64.AppImage
Icon=/home/orangepi/Pictures/obsidian.png
Type=Application
StartupNotify=true
```