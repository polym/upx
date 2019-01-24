> upx is a tool for managing files in UPYUN. Mac, Linux, Windows supported

[![Release](https://img.shields.io/badge/release-v0.2.3-orange.svg)](https://github.com/polym/upx/releases/tag/v0.2.3)
[![Build Status](https://travis-ci.org/polym/upx.svg?branch=master)](https://travis-ci.org/polym/upx)

## 基本功能

- [x] 支持基本文件系统操作命令，如 `mkdir`, `cd`, `ls`, `rm`, `pwd`
- [x] 支持上传文件或目录到又拍云存储
- [x] 支持从又拍云存储下载文件或目录到本地
- [x] 支持增量同步文件到又拍云存储
- [x] 支持删除又拍云存储中的文件或目录，并且支持通配符 `*`
- [x] 支持多用户，多操作系统
- [x] 支持基于时间列目录以及删除文件
- [x] 支持 `tree` 获取目录结构
- [x] 支持提交异步处理任务
- [x] 更加准确简洁的进度条
- [x] 使用 UPYUN GoSDK 2.1.0
- [x] 同步目录支持 --delete
- [x] 支持 CDN 缓存刷新

## 安装

### 可执行程序二进制下载地址

- [Linux 64位](http://collection.b0.upaiyun.com/softwares/upx/upx-linux-amd64-v0.2.3)
- [Linux 32位](http://collection.b0.upaiyun.com/softwares/upx/upx-linux-386-v0.2.3)
- [Windows 64位](http://collection.b0.upaiyun.com/softwares/upx/upx-windows-amd64-v0.2.3.exe)
- [Windows 32位](http://collection.b0.upaiyun.com/softwares/upx/upx-windows-386-v0.2.3.exe)
- [Mac 64位](http://collection.b0.upaiyun.com/softwares/upx/upx-darwin-amd64-v0.2.3)

### 源码编译

> 需要安装 [Golang 编译环境](https://golang.org/dl/)

```
$ git clone https://github.com/polym/upx.git
$ cd upx && make
```
or

```
$ go get github.com/polym/upx
```

### Docker

```bash
$ docker build -t upx .
$ docker run --rm upx upx -v
$ docker run --rm --volume YOUR_PATH:/go/src/upx upx upx login {Bucket} {Operator} {Password}
$ docker run --rm --volume YOUR_PATH:/go/src/upx upx upx info
```

## 使用

> 所有命令都支持 `-h` 查看使用方法

|    命令  | 说明 |
| -------- | ---- |
| login    | 登录又拍云存储 |
| logout   | 退出帐号 |
| sessions | 查看所有的会话 |
| switch   | 切换会话 |
| info     | 显示服务名、用户名等信息 |
| cd       | 改变工作目录（进入一个目录）|
| pwd      | 显示当前所在目录 |
| mkdir    | 创建目录 |
| ls       | 显示当前目录下文件和目录信息 |
| tree     | 显示目录结构 |
| get      | 下载一个文件或目录 |
| put      | 上传一个文件或目录 |
| rm       | 删除目录或文件 |
| sync     | 目录增量同步，类似 rsync |
| auth     | 生成包含空间名操作员密码信息的 auth 字符串 |
| post     | 提交异步处理任务 |
| purge    | 提交 CDN 缓存刷新任务 |


| global options | 说明 |
| -------------- | ---- |
| --quiet, -q    | 不显示信息 |
| --auth value   | auth 字符串 |
| --help, -h     | 显示帮助信息 |
| --version, -v  | 显示版本号 |


### 列目录 `ls`

> 默认按文件修改时间先后顺序输出

|  options  | 说明 |
| --------- | ---- |
| -d        | 仅显示目录 |
| -r        | 文件修改时间倒序输出 |
| --color   | 根据文件类型输出不同的颜色 |
| -c v      | 仅显示前 v 个文件或目录, 默认全部显示  |
| --mtime v | 参考 Linux `find` |

### 删除 `rm`

> 默认不会删除目录，支持通配符 `*`

|  options  | 说明 |
| --------- | ---- |
| -d        | 仅删除目录 |
| -a        | 删除目录跟文件 |
| --async   | 异步删除，目录可能需要二次删除 |
| --mtime v | 参考 Linux `find` |

### 增量同步 `sync`

> sync 本地路径 存储路径

| options  | 说明 |
| -------- | ---- |
| -w       | 指定并发数，默认为 5 |
| --delete | 删除上一次同步后本地删除的文件 |

### 生成 auth 串 `auth`

> auth 空间名 操作员 密码

当命令中包含 `--auth` 参数时，会忽略已登陆的信息。

### 提交异步任务 `post`

|     options    | 说明 |
| -------------- | ---- |
| --app value    | app 名称 |
| --notify value | 回调地址 |
| --task value   | 任务文件名 |

### 缓存刷新 `purge`

> purge url --list urls

|     options    | 说明 |
| -------------- | ---- |
| --list value   | 批量刷新文件名 |

## TODO

- [ ] put 支持断点续传
- [ ] upx 支持指定 API 地址
