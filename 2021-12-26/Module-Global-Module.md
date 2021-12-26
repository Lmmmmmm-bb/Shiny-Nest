# 模块 - 全局模块

在 Nest 中，Module 默认是将 Provider 封装在模块范围内的，所以在每次使用模块提供的程序或功能时，都需要将整个模块导入，如果有很多的地方都需要使用到一个模块时，操作就会变得非常繁琐，这里 Nest 提供了一个装饰器 `@Global()` 来解决这个问题。

使用 `@Global()` 装饰器装饰的模块只需**注册一次**就可以在其他地方直接使用而不用导入，一般在根模块即 App Module 注册即可。

## 参考

```ts
@Global()
@Module({
  controllers: [CatsController],
  providers: [CatsService],
  exports: [CatsService],
})
export class CatsModule {}
```

像上面这样装饰就可以让其他模块直接使用 `CatsService` 而不需要在模块的 `imports` 中导入。

## 建议

Nest 建议不要让所有的模块都使用 `Global()` 装饰，全局模块能减少模版代码，但是使用 `imports` 导入使模块的 Provider 提供给其他模块依旧是首选方式。
