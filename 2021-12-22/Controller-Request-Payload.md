# 控制器 - 请求载荷

在 Nest 接收参数时可以创建 DTO 对象。

DTO 是一个对象，我们可以使用 TypeScript 的 `interface` 或 `class` 来定义，Nest 建议我们使用 `class` 而不是 `interface`，因为类是 ES6 标准的一部分，在编译时会将类保留下来，而 `interface` 在编译过程会被移除，Nest 就无法在运行时对其进行引用。

定义了 DTO 之后，可以使用 DTO 作为参数类型。

## 参考

```ts
export class CreateBooksDto {
    id: string;
    name: string;
    tag: string;
}

@Post()
create(@Body() createBookDto: CreateBookDto) {
  return 'Create Book';
}
```

---

[下一章](./Controller-Example.md)
