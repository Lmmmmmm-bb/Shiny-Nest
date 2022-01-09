# 管道 - 介绍

管道是一个由 `@Injectable()` 装饰器所装饰的类，管道需要实现 `PipeTransform` 接口。

管道有两个典型的使用场景：
- **转换**：将输入的数据转换为所需的格式，进行数据的处理，比如字符串到数字。
- **验证**：验证输入的数据是否有效。

在这两种情况下，管道都对控制器路由处理程序的 `arguments` 对象进行操作。

Nest 在进入控制器 Controller 之前插入管道，管道接收到该方法的参数并对其进行操作，在这之后转换过后的参数进入路由。若管道抛出异常，则会进入异常处理层进行处理，将不会进入到路由内部。

Nest 有很多内置的管道可以使用，当然我们也可以自定义管道。

## 内置管道

内置管道均从 `@nestjs/common` 中导出。

- `ValidationPipe`
- `ParseIntPipe`
- `ParseFloatPipe`
- `ParseBoolPipe`
- `ParseArrayPipe`
- `ParseUUIDPipe`
- `ParseEnumPipe`
- `DefaultValuePipe`

## 绑定管道

下面使用 `ParseInePipe` 管道作为示例。

首先我们需要将管道绑定到适当的上下文中。

```ts
@Get(':id')
async findOne(@Param('id', ParseIntPipe) id: number) {
  return this.catsService.findOne(id);
}
```

该管道确保了以下两点
1. 进入路由的 `id` 参数确保是一个数字。
2. 如果非法参数则不会进入到路由中。

如果我们访问的地址为 `localhost:3000/abc`，则不能通过 `parseIntPipe` 转换为数字，管道将抛出异常并进入到异常处理层阻止路由处理，Nest 会返回如下响应。

```json
{
  "statusCode": 400,
  "message": "Validation failed (numeric string is expected)",
  "error": "Bad Request"
}
```

在上面的示例中我们传递了 `ParseIntPipe` 类而不是实例，Nest 将为我们进行处理。

如果我们需要传递参数对管道进行配置，那么就需要实例化对象了。

```ts
@Get(':id')
async findOne(
  @Param('id', new ParseIntPipe({ errorHttpStatusCode: HttpStatus.NOT_ACCEPTABLE }))
  id: number,
) {
  return this.catsService.findOne(id);
}
```

其他管道的工作方式类似。

## 参考

```ts
@Get()
async findOne(@Query('id', ParseIntPipe) id: number) {
  return this.catsService.findOne(id);
}

@Get(':uuid')
async findOne(@Param('uuid', new ParseUUIDPipe()) uuid: string) {
  return this.catsService.findOne(uuid);
}
```

---

[下一章](./Pipe-Custom-Pipe.md)
