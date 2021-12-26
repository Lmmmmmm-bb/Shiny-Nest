# 中间件 - 介绍

让我们跳过 *动态模块* 的部分，它会在之后的章节中详细了解。

接下来来到了下一个部分 **中间件**，相信这个概念不是第一次听说了，在 express 和 koa 等框架中也有涉及到中间件。

简单的介绍一下，中间件是在路由处理程序 **之前** 调用的函数。它能够访问 **请求和响应对象**，所以我们能通过中间件来对进入处理程序的参数等信息进行转化、修改或拦截。

## 自定义中间件

在 Nest 中可以使用函数或者带有 `Injectable()` 装饰器装饰的类中实现自定义的中间件。

如果使用类来创建自定义中间件的话，需要实现 `NestMiddleware` 接口。

下面是一个简单的使用类实现的一个中间件。

```ts
@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  use(req: Request, res: Response, next: NextFunction) {
    console.log('Request...');
    next();
  }
}
```

上面这个中间件的功能是当客户端发起请求时，在服务端打印 `Request...` 然后再使用 `next()` 将控制权移交。

在中间件中，**必须** 使用 `next()` 将控制权移交到下一个流程中，否则就无法正常结束。

## 依赖注入

因为中间件也使用了 `Injectable()` 装饰器装饰，所以也可以像 Provider 一样进行依赖注入，可参考 [Provider-Register](../2021-12-23/Provider-Register.md)。

---

[下一章](./Middleware-Applying-Middleware.md)
