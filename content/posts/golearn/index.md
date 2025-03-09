---
title: "Golang红队开发技能-1"
date: 2025-03-09T10:48:09+08:00
lastmod: 2025-03-09T10:48:09+08:00
author: ["Qiu"]

categories:
- golang
- 开发

tags:
- golang
- 开发

description: "Golang红队开发" # 文章描述，与搜索优化相关
summary: "Golang红队开发部分" # 文章简单描述，会展示在主页
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
autonumbering: true # 目录自动编号
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
searchHidden: false # 该页面可以被搜索到
showbreadcrumbs: true #顶部显示当前路径
mermaid: true
cover:
    image: ""
    caption: ""
    alt: ""
    relative: false
---

<!-- more -->

# 前言
TEst

```golang
package cmd

import (
	"fmt"
	"github.com/chainreactors/gogo/v2/core"
	"github.com/chainreactors/logs"
	"github.com/jessevdk/go-flags"
	"io/ioutil"
	"log"
	"os"
)

func init() {
	log.SetOutput(ioutil.Discard)
}

func Gogo() {
	var runner core.Runner
	defer os.Exit(0)
	parser := flags.NewParser(&runner, flags.Default)
	parser.Usage = core.Usage()
	_, err := parser.Parse()
	if err != nil {
		if err.(*flags.Error).Type != flags.ErrHelp {
			fmt.Println(err.Error())
		}
		return
	}
	if ok := runner.Prepare(); !ok {
		os.Exit(0)
	}
	logs.Log.Important(core.Banner())
	err = runner.Init()
	if err != nil {
		logs.Log.Error(err.Error())
		return
	}
	runner.Run()

	if runner.Debug {
		// debug模式不会删除.sock.lock
		logs.Log.Close(false)
	} else {
		logs.Log.Close(true)
	}
}
```

图片test

![image-20250309113353047](pic/image-20250309113353047.png)
