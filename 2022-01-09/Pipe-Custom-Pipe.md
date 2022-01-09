# 管道 - 自定义管道

Nest 提供了内置的 `ParseIntPipe` 和 `ValidationPipr`，让我们尝试从头开始构建简单的管道以了解管道的构建流程。

自定义的管道必须实现 `PipeTransform<T, R>` 接口。其中 `T` 表示输入的类型 `value`，`R` 表示管道返回的类型 `transform()`。

每个管道都必须实现 `transform()` 方法类实现 `PipeTransform` 接口。

该方法有两个参数：
1. `value`：当前处理的方法参数（路由处理方法接收之前）。
2. `metadata`：处理的方法的参数的元数据，类型为 `ArgumentMetadata`。

元数据对象具有以下属性。

```ts
export interface ArgumentMetadata {
  type: 'body' | 'query' | 'param' | 'custom';
  metatype?: Type<unknown>;
  data?: string;
}
```

各属性的意思：
1. `type`：只是参数是 body `@Body()`、query `@Query()`、param `@Param()` 还是自定义参数。
2. `metatype`：提供参数的元类型（如 `String`）。**如果在路由处理程序方法签名中省略类型声明或使用原始 JavaScript 则该值为 `undefined`。**
3. `data`：传递给装饰器的字符串。例如 `@Body('string')`，如果装饰器参数为空，则为 `undefined`。

**TypeScript 接口会在编译时被转换，建议方法参数的类型被声明为类。**

以 `ValidationPipe` 为例。

1. 首先让管道简单的接受一个输入值并返回相同的值。

```ts
import { PipeTransform, Injectable, ArgumentMetadata } from '@nestjs/common';

@Injectable()
export class ValidationPipe implements PipeTransform {
  transform(value: any, metadata: ArgumentMetadata) {
    return value;
  }
}
```

[下一章](./Pipe-Schema-Based-Validation.md)
