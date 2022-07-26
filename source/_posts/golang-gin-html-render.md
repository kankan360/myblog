---
title: 'gin HTML 渲染'
date: 2022-07-25 14:15:48
categories: 'golang'
tags: 'gin'
---


## HTML 渲染

使用 LoadHTMLGlob() 或者 LoadHTMLFiles()

```
func main() {
    router := gin.Default()
    router.LoadHTMLGlob("templates/*")
    //router.LoadHTMLFiles("templates/template1.html", "templates/template2.html")
    router.GET("/index", func(c *gin.Context) {
        c.HTML(http.StatusOK, "index.tmpl", gin.H{
            "title": "Main website",
        })
    })
    router.Run(":8080")
}
```
templates/index.tmpl
```
<html>
    <h1>
        {{ .title }}
    </h1>
</html>
```
使用不同目录下名称相同的模板
```
func main() {
    router := gin.Default()
    router.LoadHTMLGlob("templates/**/*")
    router.GET("/posts/index", func(c *gin.Context) {
        c.HTML(http.StatusOK, "posts/index.tmpl", gin.H{
            "title": "Posts",
        })
    })
    router.GET("/users/index", func(c *gin.Context) {
        c.HTML(http.StatusOK, "users/index.tmpl", gin.H{
            "title": "Users",
        })
    })
    router.Run(":8080")
}
```
templates/posts/index.tmpl
```
{{ define "posts/index.tmpl" }}
<html><h1>
    {{ .title }}
</h1>
<p>Using posts/index.tmpl</p>
</html>
{{ end }}
```
templates/users/index.tmpl
```
{{ define "users/index.tmpl" }}
<html><h1>
    {{ .title }}
</h1>
<p>Using users/index.tmpl</p>
</html>
{{ end }}
```
自定义模板渲染器
你可以使用自定义的 html 模板渲染
```
import "html/template"
func main() {
    router := gin.Default()
    html := template.Must(template.ParseFiles("file1", "file2"))
    router.SetHTMLTemplate(html)
    router.Run(":8080")
}
```
自定义分隔符
你可以使用自定义分隔
```
    r := gin.Default()
    r.Delims("{[{", "}]}")
    r.LoadHTMLGlob("/path/to/templates")
```
自定义模板功能 main.go
```
import (
    "fmt"
    "html/template"
    "net/http"
    "time"
    "github.com/gin-gonic/gin"
)
func formatAsDate(t time.Time) string {
    year, month, day := t.Date()
    return fmt.Sprintf("%d/%02d/%02d", year, month, day)
}
func main() {
    router := gin.Default()
    router.Delims("{[{", "}]}")
    router.SetFuncMap(template.FuncMap{
        "formatAsDate": formatAsDate,
    })
    router.LoadHTMLFiles("./testdata/template/raw.tmpl")
    router.GET("/raw", func(c *gin.Context) {
        c.HTML(http.StatusOK, "raw.tmpl", map[string]interface{}{
            "now": time.Date(2017, 07, 01, 0, 0, 0, 0, time.UTC),
        })
    })
    router.Run(":8080")
}
```
raw.tmpl
```
Date: {[{.now | formatAsDate}]}
```
结果：
```
Date: 2017/07/01
```