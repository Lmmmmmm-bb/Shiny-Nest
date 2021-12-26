# 中间件 - 函数中间件

在之前的章节中，我们使用 `class` 来实现了一个 LoggerMiddleware 中间件，但是这个中间件非常简单，没有类成员，没有类方法，也没有依赖项，在这个基础上我们可以将这个类中间件转换成一个函数中间件，如下。

```ts
export function logger(req: Request, res: Response, next: NextFunction) {
  console.log(`Request...`);
  next();
};
```

是不是非常简单，只需要一个函数就够了！并且它的注册和类中间件是一样的。

---

[下一章](./Middleware-Global-Middleware.md)
