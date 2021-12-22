# 控制器 - 子域名路由

在 `@Controller()` 可以传递 `host` 对象参数，在这种情况下，进入路由的请求需要满足请求头的 `Host` 字段与路由的 `host` 相匹配，否则将无法进入路由。

类似动态路由，子域名路由也可以采用动态路由的方法来获取参数。

比如 `@Controller({ host: ':prefix.lmmmmmm.cn' })` 可以匹配 `clock.lmmmmmm.cn` 等路径。

可以使用 `@HostParam(name?: string)` 装饰器来装饰参数名获取。

## 参考

以下代码示例中，请求头 `Host` 字段包含 `lmmmmmm.cn` 的请求将进入该路由，否则无法进入该路由。
```ts
@Controller({ host: 'lmmmmmm.cn' })
export class AdminController {
  @Get()
  index(): string {
    return 'Hi';
  }
}

@Controller({ host: ':prefix.lmmmmmm.cn' })
export class AccountController {
  @Get()
  getInfo(@HostParam('prefix') prefix: string) {
    return prefix;
  }
}
```

---

[下一章](./Controller-Request-Payload.md)
