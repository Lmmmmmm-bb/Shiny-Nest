# 供应商 - 服务商

在学习 Service 之前，让我们先来看看一个普通的 Service 长什么样。

```ts
@Injectable()
export class CatsService {
  private readonly cats: Cat[] = [];

  create(cat: Cat) {
    this.cats.push(cat);
  }

  findAll(): Cat[] {
    return this.cats;
  }
}

export interface Cat {
  name: string;
  age: number;
  breed: string;
}
```

从上面可以看到，一个 Service 就是一个普通的类，只不过它被 `@Injectable()` 装饰器所装饰。

再来看看 Controller 如何注入 Service。

## 基于构造函数注入

```ts
@Controller('cats')
export class CatsController {
  constructor(private catsService: CatsService) {}

  @Post()
  async create(@Body() createCatDto: CreateCatDto) {
    this.catsService.create(createCatDto);
  }

  @Get()
  async findAll(): Promise<Cat[]> {
    return this.catsService.findAll();
  }
}
```

可以看到 `CatsController` 通过类的构造函数将 `CatsService` 注入，这里的 `private` 可以立即声明和初始化。

## 基于属性的注入

如果你的类可能是别的 Provider 的父类的话，使用基于构造函数的注入可能会非常麻烦，因为你需要在子类调用 `super()` 将依赖的 Provider 向上传递，这时候基于属性的注入就会方便很多。

**一般情况下建议使用基于构造函数的注入！**

```ts
@Injectable()
export class HttpService<T> {
  @Inject('HTTP_OPTIONS')
  private readonly httpClient: T;
}
```

初始化之后就可以使用 `this.catsService` 来引用，是不是非常简单！

如何使用别的模块的 Service 会在之后提到。

---

[下一章](./Provider-Register.md)
