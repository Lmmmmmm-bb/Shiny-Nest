# 供应商 - 注册

前面我们已经完成了一个非常简单的 Service 和 Controller。

接下来我们需要让 Nest 知道我们需要这些服务，只需要在 Module 中传入相应的模块就行了。

```ts
// 方法一
// 如果你只有一个模块的话，直接在 App Module 中注册即可
@Module({
  controllers: [AppController, CatsController],
  providers: [AppService, CatsService],
})
export class AppModule {}

// 方法二
// 如果你有多个模块，可以在 App Module 中引入你的模块即可
@Module({
  imports: [UserModule],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```
