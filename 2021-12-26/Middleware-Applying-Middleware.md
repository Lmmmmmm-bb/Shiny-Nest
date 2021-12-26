# 中间件 - 应用中间件

*应用是动词。*

在 Module 中 `@Module()` 装饰器没有中间件的注册位置，需要使用 `configure()` 方法来为模块设置中间件，并且该模块必须实现 `NestModule` 接口。

讲上一章实现的自定义中间件 LoggerMiddleware 在 App Module 上设置。

## 给模块配置中间件

```ts
@Module({
  imports: [CatsModule],
})
export class AppModule implements NestModule {
  configure(consumer: MiddlewareConsumer) {
    consumer
      .apply(LoggerMiddleware)
      .forRoutes('cats');
  }
}
```

上面这个例子中，我们针对 `/cats` 路由配置了 LoggerMiddleware 中间件。

当请求进入到 `CatsController` 定义的路由时，就会调用此中间件。

## 使用对象方式配置中间件

也可以通过传入对象的方式到 `forRoutes()` 中，更细粒度的配置中间件，具体如下。

```ts
@Module({
  imports: [CatsModule],
})
export class AppModule implements NestModule {
  configure(consumer: MiddlewareConsumer) {
    consumer
      .apply(LoggerMiddleware)
      .forRoutes({ path: 'cats', method: RequestMethod.GET });
  }
}
```

上面的代码也很清晰，我们通过传入对象的方式，当请求到 `/cats` 并且是 `GET` 方法时则会调用此中间件。

## 使用通配符匹配路径

对象的 `path` 参数可以使用通配符的方式去匹配路径。

比如 `forRoutes({ path: 'ca*ts', method: RequestMethod.ALL })`，此时 `path` 可以匹配 `cats`，`cabts` 等等，`?`，`+`，`*` 和 `()` 也可以在路径中使用，并且是正则表达式对应项的子集。

例如可以使用 `(.*)` 来匹配所有路由路径。

---

[下一章](./Middleware-Middleware-Consumer.md)
