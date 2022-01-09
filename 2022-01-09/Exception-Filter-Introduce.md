# 异常过滤器 - 介绍

Nest 自带有一个负责处理程序中所有未处理的异常，当我们的程序代码为处理异常的时候，Nest 会自动捕获这个异常并且自动发送合适的响应给用户，如下。

```json
{
    "statusCode": 500,
    "message": "Internal server error"
}
```

## 标准异常

Nest 内置有 `HttpException` 类，假如在 `CatsController` 中的 `findAll()` 方法抛出了异常，如下。

```ts
@Get()
async findAll() {
  throw new HttpException('Forbidden', HttpStatus.FORBIDDEN);
}
```

则该方法会返回如下响应。

```json
{
  "statusCode": 403,
  "message": "Forbidden"
}
```

`HttpException` 构造函数有两个参数：
- `response`：定义返回的响应信息，可以是一个 `string` 或 `object`。如果提供了 `string` 类型，则会覆盖响应的 `message` 部分，如果提供的是 `object` 类型，则会覆盖整个响应主体。
- `status`：定义 HTTP 状态码，Nest 提供了 `HttpStatus` 包含各种 HTTP 状态码可供使用。

举个例子。

```ts
@Get()
async findAll() {
  throw new HttpException({
    status: HttpStatus.FORBIDDEN,
    error: 'This is a custom message',
  }, HttpStatus.FORBIDDEN);
}
```

上面这个代码访问时会返回下面的响应信息。

```json
{
  "status": 403,
  "error": "This is a custom message"
}
```

---

[下一章](./Exception-Filter-Custom-Exception.md)
