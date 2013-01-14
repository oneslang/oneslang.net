---
layout: page
title: 惯例
---

### *强制*

##### 可见性
* 包外可见:首字母大写
* 包外不可见:首字母小写

##### 测试文件命名
* 后缀:`_test`
* 例如：strings_test.go、replace_test.go、multi_test.go

##### 测试方法命名
* 前缀:`Test`
* 例如：TestMultiParse、TestParseFiles、TestParseGlob

##### 示例文件命名
* 前缀:`example`
* 后缀:`_test`
* 例如：example_test.go、examplefiles_test.go、examplefunc_test.go

##### 示例方法命名
* 前缀:`Example`
* 例如：ExampleTemplate、ExampleTemplate_glob、ExampleTemplate_share

##### 分号
* 一行单个语句:无需分号
* 一行多个语句:需要分号

##### 左大括号
* 不能将一个控制结构（if、for、switch或select）的左大括号放在下一行

### *推荐*

##### 包注释
* 使用单独文件:`doc.go`

##### Getter
* getter:Owner(不是GetOwner)
* setter:SetOwner

##### 包名
* 优:src/pkg/encoding/base64
* 劣:src/pkg/encoding/encoding_base64

##### 方法名
* 优:bufio.Reader
* 劣:bufio.BufReader

##### 接口命名
* 仅一个方法的接口名称以方法名加`-er`后缀命名：Reader、Writer、Formatter等等

