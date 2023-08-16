---
title: "Grafana 安装配置"
date: 2023-08-10T23:01:28+08:00
draft: False
tags: ["Install"]
---

Grafana docker compose 安装记录及问题总结

## 1.网上相关写法

### 1.1 docker compose

```yml
version: '3'
services:
  grafana:
    image: "grafana/grafana"
    container_name: grafana
    restart: always
    ports:
      - '3000:3000'
    volumes:
      - "./etc/data:/var/lib/grafana"
      - "./etc/grafana.ini:/etc/grafana/grafana.ini"
      - "./etc/localtime:/etc/localtime"
    environment:
            - GF_USERS_ALLOW_SIGN_UP=false
            - GF_USERS_ALLOW_ORG_CREATE=false
            - GF_USERS_AUTO_ASSIGN_ORG_ROLE=Read Only Editor 
            - GF_DATABASE_TYPE=mysql
            - GF_DATABASE_HOST=host:port
            - GF_DATABASE_NAME=grafana
            - GF_DATABASE_USER=root
            - GF_DATABASE_PASSWORD=******

```

### 1.2 字段解释

* GF_USERS_ALLOW_SIGN_UP：设置为 false 时表示禁止⽤用户注册、创建用户账号，默认为 false；但管理员用户仍然可以从 Grafana 管理界面创建用户
* GF_USERS_ALLOW_ORG_CREATE：设置为 false 禁⽌用户创建新组织，默认为 false
* GF_USERS_AUTO_ASSIGN_ORG_ROLE：新⽤户将分配给主要组织的角色，默认为 viewer，其他有效选项为 admin 和 editor
* GF_DATABASE_TYPE：数据库类型，⽆非就是 mysql、postgres 或者 sqlites
* GF_DATABASE_HOST：仅适⽤于 mysql 或 postgres，包括 ip 或主机名和端口，例如，对于 Grafana 在同一台主机上运行时 mySQL: host = 127.0.0.1 : 3306
* GF_DATABASE_NAME：Grafana 数据库名称，下述中为是定义为 grafana_test
* GF_DATABASE_USER：数据库用户，不适用于 sqlites3
* GF_DATABASE_PASSWORD：数据库⽤户密码(不适⽤于 sqlites)，如果密码中包含 # 或 ; 则必须用3个

**（以上 docker compose 及字段解释均源于网络）**

## 2.踩坑记录

上面的写法看起来没什么问题，但是在实际的部署、运行过程中存在着很多的坑

### 2.1 问题1：

can't create directory '/var/lib/grafana/plugins': Permission denied

level=error msg="alert migration failure: could not get migration log" error="failed to check table existence: dial tcp: address tcp/<25615>: unknown port"

### 2. 问题：

GF_PATHS_DATA='/var/lib/grafana' is not writable



```yml
version: '3'
services:
  grafana:
    image: grafana/grafana
    container_name: grafana
    restart: always
    ports:
      - 3000:3000
    user: '0'
    volumes:
      - /home/docker/grafana/data:/var/lib/grafana
      - /home/docker/grafana/plugins:/var/lib/grafana/plugins

    environment:
            - GF_DATABASE_TYPE=mysql
            - GF_DATABASE_HOST=
            - GF_DATABASE_PORT=
            - GF_DATABASE_NAME=grafana
            - GF_DATABASE_USER=root
            - GF_DATABASE_PASSWORD=*******
```