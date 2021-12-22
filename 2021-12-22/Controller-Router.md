# 控制器 - 路由

## 控制器装饰器

使用 `@Controller(router-path?: string = '/')` 装饰器装饰一个 `class` 来创建一个 Nest 路由。

可以通过命令行来自动创建路由。
```
$ nest g controller [router-path]
```

这里我们称 `router-path` 为路由的**主路径**，后面我们会提到**补充路径 `path`**。

如果我们没有给装饰器提供 `router-path` 参数，则默认为 `/`。假设 Nest 运行在 **3000** 端口，使用 `@Controller()` 创建一个根路由，即路由的主路径为 `/`。

同理，如果提供了参数，那么路由的主路径就是提供的路径。

### 参考

- `@Controller()` => `localhost:3000/`
- `@Controller('book')` => `localhost:3000/book`
- `@Controller('api/book')` => `localhost:3000/api/book`

## 请求方法装饰器

请求方法装饰器用来装饰 `class` 的一个方法，方法名不具有任何意义，意味着你可以将方法名任意命名，但是为了代码的可读性和可维护性建议将方法命名为与控制器相关联的名字。

可以使用 `@Get()`, `@Post()`, `@Put()`, `@Delete()`, `@Patch()`, `@Options()`, `@Head()` 装饰器来告诉 Nest 该路由的请求方法。

同时，每个装饰器可以提供一个 `path` 字符串参数，这个 `path` 就是路由的**补充路径**了。最后的路由路径将会和**主路径**拼接，即 `localhost:${port}/${router-path}/${path}`。

和控制器装饰器一样，如果没有提供 `path` 参数，则默认为 `/`。

可以使用动态参数传递信息。比如 `@Get('query/:id')` 可以匹配到 `localhost:3000/api/book/query/*`。

### 参考

假设此时的的 `class` 被 `@Controller('api/book')` 所装饰。
- `@Get()` => `Get localhost:3000/api/book`
- `@Post()` => `Post localhost:3000/api/book`
- `@Get('all')` => `Get localhost:3000/api/book/all`

## 路由通配符

请求方法装饰器可以使用正则的通配符。

比如 `@Get('b*k')` 可以匹配到 `bk`, `bak`, `babck` 等等，除此之外还有 `?`, `+`, `()` 可以在路径中使用。

---

- [下一章](./Controller-Request-Object.md)
