# 中间件 - 全局中间件

如果想将中间件应用到全部路由上，可以使用 Nest 实例的 `use()` 方法。

```ts
const app = await NestFactory.create(AppModule);
app.use(logger);
await app.listen(3000);
```

使用 `use()` 应用全局中间件无法访问 DI 容器，所以也可以使用 `.forRoutes('*')` 的方法在 App Module 注册，将其应用到所有路由上。
