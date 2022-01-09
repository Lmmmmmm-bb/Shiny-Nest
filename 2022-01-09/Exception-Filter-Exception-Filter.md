# 异常过滤器 - 异常过滤器

Nest 文档中在这一章的前面讲了很多关于 HTTP 异常的内容，就是为这一部分做准备。

下面来讲讲 **异常过滤器**。

大部分时候内置的异常过滤器可以处理很多情况，我们也可以根据自己的需求来创建自己的异常过滤器。

首先让我们来创建一个负责捕获 `HttpException` 类实例异常的异常过滤器，该异常过滤器用来添加日志记录并返回响应，并为它们自定义响应逻辑，为此我们需要访问底层对象 `Request` 和 `Response`。

从 `Request` 中获取 `url` 并保存在日志中，使用 `Response` 对象的 `json` 方法控制响应信息。

```ts
import { ExceptionFilter, Catch, ArgumentsHost, HttpException } from '@nestjs/common';
import { Request, Response } from 'express';

@Catch(HttpException)
export class HttpExceptionFilter implements ExceptionFilter {
  catch(exception: HttpException, host: ArgumentsHost) {
    const ctx = host.switchToHttp();
    const response = ctx.getResponse<Response>();
    const request = ctx.getRequest<Request>();
    const status = exception.getStatus();

    response
      .status(status)
      .json({
        statusCode: status,
        timestamp: new Date().toISOString(),
        path: request.url,
      });
  }
}
```

所有的异常过滤器都需要实现 `Exception<T>` 接口，该接口提供 `catch(exception: T, host: ArgumentsHost)` 方法，其中 `T` 表示异常类型。

`@Catch(HttpException)` 装饰器结合所需的元数据（这里是 `HttpException`）告诉 Nest 这个过滤器匹配 `HttpException` 类型的异常。

`@Catch()` 装饰器可以采用单个参数或逗号分隔的列表。
