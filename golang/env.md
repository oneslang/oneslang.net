---
layout: page
title: 环境
---

### 环境变量

* GOROOT  
`go安装包的根目录`
* GOPATH  
`外部包安装的根目录。go build和go install利用$GOPATH寻找软件需要编译和链接的关联包。必须先安装外部包才能使用。命令go get会在$GOPATH目录中安装源代码并且编译包`
* GOOS  
`目标代码的操作系统，与当前使用平台无关，用于交叉编译，选项有windows、linux、freebsd、darwin`
* GOARCH  
`目标代码的CPU类型，与当前使用平台无关，用于交叉编译，选项有amd64、386、arm`
* GOBIN  
`go的二进制程序目录。如果是没设置$GOBIN环境变量，则默认是安装在$HOME/bin。如果设置了该变量，需要确保$PATH变量也包含这个路径，这样编译器可以找到正确的执行文件`

### GO工具

* build		`编译包`
* clean		`清除目标文件`
* doc		`生成文档`
* fix		`升级修复为最新版语法`
* fmt		`格式化代码`
* get		`下载并安装依赖`
* install	`编译并安装依赖`
* list		`包的列表`
* run		`构建并执行应用`
* test		`测试包`
* tool		`调用扩展工具`
* version	`显示GO版本`

### 常用命令

* 本地化文档(golang.org的本地copy版本)  
命令行执行：`godoc -http=:6060`  
浏览器打开：`127.0.0.1:6060`

