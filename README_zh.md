# go-captcha - Behavioral Verification Code

[![Go Report Card](https://goreportcard.com/badge/github.com/wenlng/go-captcha?t=1)](https://goreportcard.com/report/github.com/wenlng/go-captcha)
[![Version](https://img.shields.io/github/tag/wenlng/go-captcha.svg)](https://github.com/wenlng/go-captcha/releases)
[![GoDoc](https://godoc.org/github.com/wenlng/go-captcha?status.svg)](https://godoc.org/github.com/wenlng/go-captcha)
[![License](https://img.shields.io/github/license/wenlng/go-captcha.svg)](https://github.com/wenlng/go-captcha/blob/master/LICENSE)

> [English](README.md) | 中文

go-captcha, 一个简洁易用、交互友好、高安全性的点选行为验证码 Go 库 ，采用 “验证码展示-采集用户行为-验证行为数据” 为流程，用户无需键盘手动输入，极大优化传统验证码用户体验不佳的问题，支持PC端及移动端，带有与前端交互的DEMO。. 

- Github：[https://github.com/wenlng/go-captcha](https://github.com/wenlng/go-captcha)
- 实例代码：[https://github.com/wenlng/go-captcha-example](https://github.com/wenlng/go-captcha-example)
- Demo：[http://47.104.180.148:8081/go_captcha_demo](http://47.104.180.148:8081/go_captcha_demo)
- 作者网站: [http://witkeycode.com](http://witkeycode.com)

<br/>

<div align="center">
    <img src="http://47.104.180.148/go-captcha/go-captcha-01.png?v=2" alt="Reward Support">
    <br/>
    <br/>
    <img src="http://47.104.180.148/go-captcha/go-captcha-02.png?v=1" alt="Reward Support">
    <br/>
    <br/>
    <img src="http://47.104.180.148/go-captcha/go-captcha.jpg?v=1" alt="Reward Support">
    <br/>
    <br/>   
</div>

## 中国Go模块代理
- GoProxy https://github.com/goproxy/goproxy.cn
- AliProxy： https://mirrors.aliyun.com/goproxy/
- OfficialProxy： https://goproxy.io/
- ChinaProxy：https://goproxy.cn
- Other：https://gocenter.io

#### 设置Go模块的代理
- Window
```shell script
set GO111MODULE=on
set GOPROXY=https://goproxy.io,direct

### Golang 1.13+ 可以直接执行
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.io,direct
```
- Linux or Mac
```shell script
vi vim ~/.bash_profile
export GO111MODULE=on
export GOPROXY=https://goproxy.io,direct
source ~/.bash_profile
```

### 依赖golang官方标准库
```
go get -u github.com/golang/freetype
go get -u golang.org/x/crypto
go get -u golang.org/x/image
```

### 安装模块
```
go get -u github.com/wenlng/go-captcha
```

### 引入模块
```go
package main

import "github.com/wenlng/go-captcha/captcha"

func main(){
   // ....
}
```

### 快速使用
在生成验证码数据时 SetFont 和 SetBackground 配置是必须要先配置
<br/>
你可以直接拷贝实例中 "__example/resources" 的图片和字体文件到你的项目中使用
```go
package main
import (
    "fmt"
    "os"
    "github.com/wenlng/go-captcha/captcha"
)

func main(){
    // Captcha Single Instances
    capt := captcha.GetCaptcha()
    
    path, _ := os.Getwd()
    // ==========================
    // 必须设置
    // --------------------------
    // 设置验证码字体
    capt.SetFont([]string{
        path + "/__example/resources/fonts/fzshengsksjw_cu.ttf",
        path + "/__example/resources/fonts/fzssksxl.ttf",
    })
    
    // 设置验证码背景图
    capt.SetBackground([]string{
        path + "/__example/resources/images/1.jpg",
        path + "/__example/resources/images/2.jpg",
    })
    
    // 生成验证码
    dots, b64, tb64, key, err := capt.Generate()
    if err != nil {
        panic(err)
        return
    }
    
    // 主图base64
    fmt.Println(len(b64))
    
    // 缩略图base64
    fmt.Println(len(tb64))
    
    // 唯一key
    fmt.Println(key)
    
    // 文本位置验证数据
    fmt.Println(dots)
}

```

### 验证码实例
- 创建实例或者获取单例模式的实例
```go
package main
import (
    "fmt"
    "github.com/wenlng/go-captcha/captcha"
)

func main(){
	// 创建验证码实例
    // capt := captcha.NewCaptcha() 
    
    // 单例模式的验证码实例
    capt := captcha.GetCaptcha()

    // ====================================================
    fmt.Println(capt)

}
```

### 验证码配置
#### 文本相关的配置
```go
package main
import (
    "fmt"
    "github.com/wenlng/go-captcha/captcha"
)

func main(){
    capt := captcha.GetCaptcha()
    
    // ====================================================
    // Method: SetRangChars (chars []string) error;
    // Desc: Set random char of captcha
    // ====================================================
    // Letter
    //chars := "abcdefghijklmnopqrstuvwxyz0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    //_ = capt.SetRangChars(strings.Split(chars, ""))
    
    // Two Letter
    //chars := []string{"HE","CA","WO","NE","HT","IE","PG","GI","CH","CO","DA"}
    //_ = capt.SetRangChars(chars)

    // Chinese Char
    chars := []string{"你","好","呀","这","是","点","击","验","证","码","哟"}
    _ = capt.SetRangChars(chars)

    // ====================================================
    fmt.Println(capt)
}
```

#### 图片相关的配置
```go
package main
import (
    "fmt"
    "os"
    "github.com/wenlng/go-captcha/captcha"
)

func main(){
    capt := captcha.GetCaptcha()
    
    path, _ := os.Getwd()    
    // ====================================================
    // Method: SetBackground(color []string);
    // Desc: 设置验证码背景图
    // ====================================================
    capt.SetBackground([]string{
        path + "/__example/resources/images/1.jpg",
        path + "/__example/resources/images/2.jpg",
    })

    // ====================================================
    // Method: SetFont(fonts []string);
    // Desc: 设置验证码字体
    // ====================================================
    capt.SetFont([]string{
        path + "/__example/resources/fonts/fzshengsksjw_cu.ttf",
        path + "/__example/resources/fonts/fzssksxl.ttf",
    })

    // ====================================================
    // Method: SetImageSize(size *Size);
    // Desc: 设置验证码主图的尺寸
    // ====================================================
    capt.SetImageSize(&captcha.Size{300, 300})

    // ====================================================
    // Method: SetThumbSize(size *Size);
    // Desc: 设置验证码缩略图的尺寸
    // ====================================================
    capt.SetThumbSize(&captcha.Size{150, 40})

    // ====================================================
    // Method: SetFontDPI(val int);
    // Desc: 设置验证码字体的随机DPI，最好是72
    // ====================================================
    capt.SetFontDPI(72)

    // ====================================================
    // Method: SetTextRangLen(val *captcha.RangeVal);
    // Desc: 设置验证码文本总和的随机长度范围
    // ====================================================
    capt.SetTextRangLen(&captcha.RangeVal{6, 7})

    // ====================================================
    // Method: SetRangFontSize(val *captcha.RangeVal);
    // Desc: 设置验证码文本的随机大小
    // ====================================================
    capt.SetRangFontSize(&captcha.RangeVal{32, 42})

    // ====================================================
    // Method: SetRangCheckTextLen(val *captcha.RangeVal);
    // Desc:设置验证码校验文本的随机长度的范围
    // ====================================================
    capt.SetRangCheckTextLen(&captcha.RangeVal{2, 4})

    // ====================================================
    // Method: SetRangCheckFontSize(val *captcha.RangeVal);
    // Desc:设置验证码文本的随机大小
    // ====================================================
    capt.SetRangCheckFontSize(&captcha.RangeVal{24, 30})
    
    // ====================================================
    // Method: SetTextRangFontColors(colors []string);
    // Desc: 设置验证码文本的随机十六进制颜色
    // ====================================================
    capt.SetTextRangFontColors([]string{
        "#1d3f84",
        "#3a6a1e",
    })

    // ====================================================
    // Method: SetImageFontAlpha(val float64);
    // Desc:设置验证码字体的透明度
    // ====================================================
    capt.SetImageFontAlpha(0.5)

    // ====================================================
    // Method: SetTextRangAnglePos(pos []*RangeVal);
    // Desc:设置验证码文本的角度
    // ====================================================
    capt.SetTextRangAnglePos([]*captcha.RangeVal{
        {1, 15},
        {15, 30},
        {30, 45},
        {315, 330},
        {330, 345},
        {345, 359},
    })

    // ====================================================
    // Method: SetImageFontDistort(val int);
    // Desc:设置验证码字体扭曲程度
    // ====================================================
    capt.SetImageFontDistort(captcha.ThumbBackgroundDistortLevel2)
  
    // ====================================================
    // Method: SetThumbBgColors(colors []string);
    // Desc: 设置缩略验证码背景的随机十六进制颜色
    // ====================================================
    capt.SetThumbBgColors([]string{
        "#1d3f84",
        "#3a6a1e",
    })

    // ====================================================
    // Method: SetThumbBackground(colors []string);
    // Desc:设置缩略验证码随机图像背景
    // ====================================================
    capt.SetThumbBackground([]string{
        path + "/__example/resources/images/r1.jpg",
        path + "/__example/resources/images/r2.jpg",
    })

    // ====================================================
    // Method: SetThumbBgDistort(val int);
    // Desc:设置缩略验证码的扭曲程度
    // ====================================================
    capt.SetThumbBgDistort(captcha.ThumbBackgroundDistortLevel2)

    // ====================================================
    // Method: SetThumbBgCirclesNum(val int);
    // Desc:设置验证码背景的圈点数
    // ====================================================
    capt.SetThumbBgCirclesNum(20)

    // ====================================================
    // Method: SetThumbBgSlimLineNum(val int);
    // Desc:设置验证码背景的线条数
    // ====================================================
    capt.SetThumbBgSlimLineNum(3)
    

    // ====================================================
    fmt.Println(capt)
}
```

### 生成验证码数据
```go
package main
import (
    "fmt"
    "os"
    "github.com/wenlng/go-captcha/captcha"
)

func main(){
    capt := captcha.GetCaptcha()
    
    path, _ := os.Getwd()
    // set configuration ...
    // ==========================
    capt.SetFont([]string{
        path + "/__example/resources/fonts/fzshengsksjw_cu.ttf",
        path + "/__example/resources/fonts/fzssksxl.ttf",
    })
    capt.SetBackground([]string{
        path + "/__example/resources/images/1.jpg",
        path + "/__example/resources/images/2.jpg",
    })
    
    // generate ...
    // ====================================================
    // dots:  文本字符的位置信息
    //  - {"0":{"Index":0,"Dx":198,"Dy":77,"Size":41,"Width":54,"Height":41,"Text":"SH","Angle":6,"Color":"#885500"} ...}
    // imageBase64:  Verify the clicked image
    // thumbImageBase64: Thumb displayed
    // key: Only Key
    // ====================================================
    dots, imageBase64, thumbImageBase64, key, err := capt.Generate()
    if err != nil {
        panic(err)
        return
    }
    fmt.Println(len(imageBase64))
    fmt.Println(len(thumbImageBase64))
    fmt.Println(key)
    fmt.Println(dots)
}
```

### 在 __example 中的前端在数据请求或提交验证数据时的格式： 
```
// Example: 获取验证码数据
API = http://....../captcha/captcha-data
    Respose Data = {
        "code": 0,
        "image_base64": "...",
        "thumb_base64": "...",
        "captcha_key": "...",
    }     

// Example: 提交校验数据 
API = http://....../captcha/check-data
    Request Data = {
        dots: "x1,y1,x2,y2,...."
        key: "......"
    }
```
<br/>

<div align="center">
    <img src="http://47.104.180.148/reward-support.png?v=1" alt="Reward Support">
</div>
<br/>

## LICENSE
    MIT