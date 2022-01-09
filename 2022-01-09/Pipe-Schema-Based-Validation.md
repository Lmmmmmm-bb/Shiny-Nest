# 管道 - 基于模式验证

上一章中我们实现了一个 `ValidationPipe`，目前它的功能只是将参数直接传递到控制器中，为了方便我将上一章实现的代码放在这里方便查看。

```ts
import { PipeTransform, Injectable, ArgumentMetadata } from '@nestjs/common';

@Injectable()
export class ValidationPipe implements PipeTransform {
  transform(value: any, metadata: ArgumentMetadata) {
    return value;
  }
}
```

让我们的管道更有用处一点。

首先来看看 `CatsController` 的 `create()` 方法。

```ts
@Post()
async create(@Body() createCatDto: CreateCatDto) {
  this.catsService.create(createCatDto);
}
```

我们希望传入的 `createCatDto` 对象是有效对象，其中 `CreateCatDto` 定义如下。

```ts
export class CreateCatDto {
  name: string;
  age: number;
  breed: string;
}
```

为了确保传入 `create()` 方法请求对象是有效的，我们需要验证 `createCatDto` 对象的三个成员。

虽然能够在控制器中手动的验证，但这样不利于代码的维护，一旦对象成员很多，验证代码将会非常庞大，这种情况正是管道解决的。
