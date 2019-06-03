# gpy

[![CircleCI Status](https://circleci.com/gh/yanjingang/gpy.svg?style=shield)](https://circleci.com/gh/yanjingang/gpy)
[![Build Status](https://travis-ci.org/yanjingang/gpy.svg?branch=master)](https://travis-ci.org/yanjingang/gpy)<!-- [![Coverage Status](https://coveralls.io/repos/gtihub.com/yanjingang/gpy/badge.svg?branch=master)](https://coveralls.io/r/github.com/yanjingang/gpy?branch=master) -->
[![codecov](https://codecov.io/gh/yanjingang/gpy/branch/master/graph/badge.svg)](https://codecov.io/gh/yanjingang/gpy)
[![Go Report Card](https://goreportcard.com/badge/github.com/yanjingang/gpy)](https://goreportcard.com/report/github.com/yanjingang/gpy)
[![GoDoc](https://godoc.org/github.com/yanjingang/gpy?status.svg)](https://godoc.org/github.com/yanjingang/gpy)

汉语拼音转换工具 Go 版。


## Installation

```
go get -u github.com/yanjingang/gpy
```

### install CLI tool:

```
go get -u github.com/yanjingang/gpy/pinyin
$ gpy 中国人
zhōng guó rén
```


## Documentation

API documentation can be found here:
[godoc](https://godoc.org/github.com/yanjingang/gpy)


## Usage

```go
package main

import (
	"fmt"

	"github.com/yanjingang/gpy"
)

func main() {
	hans := "中国人"

	// 默认
	a := gpy.NewArgs()
	fmt.Println(gpy.Pinyin(hans, a))
	// [[zhong] [guo] [ren]]

	// 包含声调
	a.Style = gpy.Tone
	fmt.Println(gpy.Pinyin(hans, a))
	// [[zhōng] [guó] [rén]]

	// 声调用数字表示
	a.Style = gpy.Tone2
	fmt.Println(gpy.Pinyin(hans, a))
	// [[zho1ng] [guo2] [re2n]]

	// 开启多音字模式
	a = gpy.NewArgs()
	a.Heteronym = true
	fmt.Println(gpy.Pinyin(hans, a))
	// [[zhong zhong] [guo] [ren]]
	a.Style = gpy.Tone2
	fmt.Println(gpy.Pinyin(hans, a))
	// [[zho1ng zho4ng] [guo2] [re2n]]

	fmt.Println(gpy.LazyPinyin(hans, gpy.NewArgs()))
	// [zhong guo ren]

	fmt.Println(gpy.Convert(hans, nil))
	// [[zhong] [guo] [ren]]

	fmt.Println(gpy.LazyConvert(hans, nil))
	// [zhong guo ren]
}
```


## Related Projects

* [hotoo/pinyin](https://github.com/hotoo/pinyin): 汉语拼音转换工具 Node.js/JavaScript 版。
* [mozillazg/python-pinyin](https://github.com/mozillazg/python-pinyin): 汉语拼音转换工具 Python 版。
* [mozillazg/rust-pinyin](https://github.com/mozillazg/rust-pinyin): 汉语拼音转换工具 Rust 版。


## License

Under the MIT License, base on [go-pinyin](https://github.com/mozillazg/go-pinyin).
