# 异常过滤器 - 自定义异常

大部分情况下，Nest 内置的异常已经足够我们使用，当然我们也可以通过创建自定义异常来创建自己的异常层次结构。

自定义异常继承自 `HttpException` 类，这样 Nest 会识别自定义的异常并自动处理响应。

创建一个 `Forbidden Exception` 并在 `CatsController` 中使用。

为了方便我将其写在一起。

```ts
export class ForbiddenException extends HttpException {
  constructor() {
    super('Forbidden', HttpStatus.FORBIDDEN);
  }
}

@Get()
async findAll() {
  throw new ForbiddenException();
}
```

---

[下一章](./Exception-Filter-Nest-Exception.md)
