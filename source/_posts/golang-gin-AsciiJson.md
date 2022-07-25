---
title: 'gin AsciiJSON'
date: 2022-07-25 14:05:48
categories: 'golang'
tags: 'gin'
---


## AsciiJSON

使用 AsciiJSON 生成具有转义的非 ASCII 字符的 ASCII-only JSON。

```
func main() {
    r := gin.Default()
    r.GET("/someJSON", func(c *gin.Context) {
        data := map[string]interface{}{
            "lang": "GO语言",
            "tag":  "<br>",
        }
        // 输出 : {"lang":"GO\u8bed\u8a00","tag":"\u003cbr\u003e"}
        c.AsciiJSON(http.StatusOK, data)
    })
    // 监听并在 0.0.0.0:8080 上启动服务
    r.Run(":8080")
}
```