---
layout: page
title: 惯例
---

### *强制*

##### 可见性
* 包外可见：首字母大写
* 包外不可见：首字母小写

##### 测试文件命名
* 后缀：`_test`
* 例如：strings_test.go、replace_test.go、multi_test.go

##### 测试方法命名
* 前缀：`Test`
* 例如：TestMultiParse、TestParseFiles、TestParseGlob

##### 示例文件命名
* 前缀：`example`
* 后缀：`_test`
* 例如：example_test.go、examplefiles_test.go、examplefunc_test.go

##### 示例方法命名
* 前缀：`Example`
* 例如：ExampleTemplate、ExampleTemplate_glob、ExampleTemplate_share

##### 分号
* 一行单个语句：无需分号
* 一行多个语句：需要分号

##### 左大括号
* 不能将一个控制结构（if、for、switch或select）的左大括号放在下一行

### *推荐*

##### 包注释
* 使用单独文件：`doc.go`

##### Getter
* getter：Owner(不是GetOwner)
* setter：SetOwner

##### 包名
* 优：src/pkg/encoding/base64
* 劣：src/pkg/encoding/encoding_base64

##### 方法名
* 优：bufio.Reader
* 劣：bufio.BufReader

##### 接口命名
* 仅一个方法的接口命名方式：`方法名+er`
* 例如：Reader、Writer、Formatter等等

##### 构造器
* 前缀：New
* 单个构造器时：New
* 例如：errors.New、template.New、ring.New
* 多个构造器时：New*
* 例如：time.NewTimer、time.NewTicker、image.NewGray、image.NewRGBA

### *可选*

##### 项目源码路径
* 源码直接放在项目根目录下
* 而不是src目录或其他目录
* 参考：github.com/oneslang/db

##### 项目包文件命名
* 分类从大到小
* 分割符使用`.`
* 例如：api.factory.go、api.session.go、core.factory.go、core.session.go
* 参考：github.com/oneslang/db

##### 项目版本
* 1.0：github.com/oneslang/db
* 2.0：github.com/oneslang/db2
* 3.0：github.com/oneslang/db3

