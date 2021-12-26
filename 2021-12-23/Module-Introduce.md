# 模块 - 介绍

模块 Module 是用来组织 Controller 和 Provider 的一个类，它被 `@Module(metadata?: ModuleMetadata)` 装饰器装饰。

一个 Nest 应用程序必须有一个根模块即 App Module，所有其他的模块都以 App Module 为起点，但是如果你的程序比较简单，仅有一个 App Module 也是可行的。

## Module Meta Data 对象

`@Module()` 可以传入一个 `ModuleMetadata` 类型的对象，该对象的所有属性都是可选属性。

- `providers`
- `controllers`
- `imports`
- `exports`

对于前三个属性之前也有提到过了，这里简单讲一下 `exports` 属性。

对于一个模块来说，默认封装当前模块的所有供应商 Provider，**其他模块不能注入既不属于自己模块也不是别的模块导出的 Provider**。

上面那句话可能有点绕，简单来说我这个模块不能导入其他模块的 Provider，除非其他模块有进行导出。

那么如何导出，就用到了 `exports` 这个属性了，只需要把别的模块要用到的 Provider 传入 `exports` 数组即可。

---

[下一页](../2021-12-26/Module-Dependency-Injection.md)
