# 供应商 - 介绍

上次学习了 [控制器 Controller](../2021-12-22/Controller-Router.md)，今天按照顺序就来学习另一个重点**供应商 Provider**。

发起一个请求，首先会进入到特定的 Controller 来进行请求处理的流程，进入到 Controller 之后，一般来说不会把所有的东西都写在 Controller 中，而是把这些处理的流程细化和抽象，变成一个个可复用的方法或函数，那我们就称这些可复用的方法或函数为**服务商 Service**。

**Service** 可以被不同的 Controller，也可以注入到其他的模块中被其他模块使用，当然这部分是后面才会学习的了，现在我们只需要知道，Service 可能会被同一个 Controller 的不同路由使用。

---

[下一章](./Provider-Service.md)
