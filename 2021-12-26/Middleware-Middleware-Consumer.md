# 中间件 - 中间件消费者

中间件消费者即 `MiddlewareConsumer` 类，它提供了多种方法来管理中间件。

`forRoutes()` 方法可以传入单个字符串、多个字符串、`RouteInfo` 对象、一个或多个 Controller。

`apply()` 可以传入单个或多个中间件，这些中间件会按照传入的顺序执行。

`exclude()` 用来配置需要从中间件中排除哪些路由，可以传入单个字符串、多个字符串、`RouteInfo` 对象进行配置，并且同样支持路由通配符。

## 参考

```ts
@Module({
  imports: [CatsModule],
})
export class AppModule implements NestModule {
  configure(consumer: MiddlewareConsumer) {
    consumer
      .apply(cors(), helmet(), LoggerMiddleware)
      .exclude(
        { path: 'cats', method: RequestMethod.GET },
        { path: 'cats', method: RequestMethod.POST },
        'cats/(.*)',
      )
      .forRoutes(CatsController);
  }
}
```

---

[下一章](./Middleware-Function-Middleware.md)
