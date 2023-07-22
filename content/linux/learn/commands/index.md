---

title: "Linux 常用命令"
date: 2023-07-22T16:29:21+08:00
draft: False
tags: ["Commands"]

---

总结常用的 Linux 系统命令

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
```