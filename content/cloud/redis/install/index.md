---
title: "Redis 安装配置"
date: 2023-08-09T23:33:07+08:00
draft: False
tags: ["Install"]
---

Redis docker compose 安装记录

```
version: "3.0"
services:
  redis:
    image: redis
    ports:
      - 6379:6379
    volumes:
      #Redis持久化数据映射
      - /home/docker/redis/data:/data
      #准备自己的redis配置文件，包含redis连接密码
      - /home/docker/redis/config:/etc/redis/redis.conf
      #redis存储路径
      - /home/docker/redis/logs:/logs
      # 容器启动后在容器中执行的命令，启动redis,appendonly参数可用来持久化redis数据参数
      # 覆盖容器启动后默认执行的命令
    # command: redis-server /usr/local/etc/redis/redis.conf
    command: redis-server --requirepass ******
    restart: always
```