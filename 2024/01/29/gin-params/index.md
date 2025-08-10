# Gin 框架获取请求参数的方式




## GET

使用 Query，请求中参数直接拼接在 url 中

```
http://localhost:8888/v1/user/get?id=9
```

router

```
userv1.GET("/get", userHandler.Get)
```

参数绑定

```go
idParam := c.Query("id")
```



## POST-JSON

```go
var req entity.User

	if err := c.ShouldBindJSON(&req); err != nil {
		response.Failed(c, code.ErrBind, err.Error())
		return
	}
```



绑定方式有两种，Gin 官方文档是这么描述的：

Gin提供了两类绑定方法：

- Type

  \- Must bind

  - **Methods** - `Bind`, `BindJSON`, `BindXML`, `BindQuery`, `BindYAML`
  - **Behavior** - 这些方法属于 `MustBindWith` 的具体调用。 如果发生绑定错误，则请求终止，并触发 `c.AbortWithError(400, err).SetType(ErrorTypeBind)`。响应状态码被设置为 400 并且 `Content-Type` 被设置为 `text/plain; charset=utf-8`。 如果您在此之后尝试设置响应状态码，Gin会输出日志 `[GIN-debug] [WARNING] Headers were already written. Wanted to override status code 400 with 422`。 如果您希望更好地控制绑定，考虑使用 `ShouldBind` 等效方法。

- Type

  \- Should bind

  - **Methods** - `ShouldBind`, `ShouldBindJSON`, `ShouldBindXML`, `ShouldBindQuery`, `ShouldBindYAML`
  - **Behavior** - 这些方法属于 `ShouldBindWith` 的具体调用。 如果发生绑定错误，Gin 会返回错误并由开发者处理错误和请求。

使用 Bind 方法时，Gin 会尝试根据 Content-Type 推断如何绑定。 如果你明确知道要绑定什么，可以使用 `MustBindWith` 或 `ShouldBindWith`。****



## URL参数

```go
 // 使用URL参数并获取参数
    router.GET("/user/:username/:password", func(c *gin.Context) {
        // 使用Param获取URL参数
        username := c.Param("username")
        password := c.Param("password")

        // 返回请求参数
        c.JSON(200, gin.H{
            "username": username,
            "password": password,
        })
    })
```


