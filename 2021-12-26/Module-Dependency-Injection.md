# 模块 - 依赖注入

一个 Module 注册了 Provider 之后怎么进行注入，使得能够在程序中使用 Provider 提供的各种功能。

可以参考以下代码。

```ts
@Module({
  controllers: [CatsController],
  providers: [CatsService],
})
export class CatsModule {
  constructor(private catsService: CatsService) {}
}
```

由于**循环依赖**，模块本身不能作为 Provider 注入。

---

[下一页](./Module-Global-Module.md)
