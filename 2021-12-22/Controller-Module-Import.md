# 控制器 - 引入

在 [完全定义控制器](./Controller-Example.md) 之后，Nest 仍然不知道控制器的存在，我们需要引入控制器到模块中才能正常使用。

控制器总是属于一个模块，我们需要将 Controller 引入到 Module 中。

使用 `@Module()` 装饰器将控制器引入。

## 参考

```ts
import { Module } from '@nestjs/common';
import { CatsController } from './cats/cats.controller';

@Module({
  controllers: [CatsController],
})
export class AppModule {}
```
