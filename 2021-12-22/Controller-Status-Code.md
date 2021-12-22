# 控制器 - 状态码

在 Nest 中，响应的状态码都是 `200`，除了 `Post` 请求是 `201`。

可以通过 `@HttpCode(status: number)` 来控制响应状态码。
