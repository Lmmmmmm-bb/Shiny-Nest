# 控制器 - 重定向

可以使用 `@Redirect(url?: string, statusCode?: number)` 来将响应重定向到指定的 URL。

其中 `statusCode` 默认响应代码为 `302`。

## 动态重定向

如果需要动态重定向的话，可以在请求方法返回一个特定的对象。
```ts
{
    url: string,
    statusCode: number
}
```
返回值将覆盖 `@Redirect()` 的传递参数。

### 参考

```ts
@Get('docs')
@Redirect('https://docs.nestjs.com', 302)
getDocs(@Query('version') version) {
  if (version && version === '5') {
    return { url: 'https://docs.nestjs.com/v5/' };
  }
}
```
