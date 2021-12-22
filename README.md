# docker-compose lnmp


# .env config
请务必在.env文件配置自己得路径


# log dir,data dir
请自行创建log目录 data目录


# docker-compose version 1.26.2
高版本将会构建不成功
安装参考
```
curl -L https://get.daocloud.io/docker/compose/releases/download/1.26.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```


# 建议关闭selinux
这会导致docker映射后，服务无法访问映射目录

