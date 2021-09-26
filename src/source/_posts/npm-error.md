---
title: NPM使用时的一些错误问题解决
date: 2021-06-22 17:09:56
---

# npm WARN tar invalid entry
检查本地npm配置
``` bash
npm config ls
```
检查对应的proxy和registery是否正确，如果不正确请修改 如果配置正确，则检查项目目录下是否有 .npmrc 配置文件，此配置文件会覆盖全局的配置

# npm WARN tar zlib error: unexpected end of file
``` bash
npm install --no-package-lock
```