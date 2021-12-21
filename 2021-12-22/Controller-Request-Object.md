# 控制器 - 请求对象

Nest 提供了很对封装好的装饰器来获取不同请求对象的参数。

主要为一下几种。

- `@Param(key?: string)`
- `@Body(key?: string)`
- `@Query(key?: string)`
- `@Headers(name?: string)`
- `@Ip()`
- `@HostParam()`

[查看全部请求对象装饰器](https://docs.nestjs.com/controllers)

如果没有提供相应的参数，则默认获取整个对象。

相对而言，如果提供了参数，则会获取对应请求对象的同名字段。

## 参考

Controller Router: `@Controller('api/book')` & `@Get('query/:id')`

Request Address: `localhost:3000/api/book/12138?name=ninja`

Body (`x-www-form-urlencoded`): `tag=js`

Header: `token=Bearer Token`

- `@Param()` => `{ id: '12138' }`
- `@Param('id')` => `'12138'`
- `@Body()` => `{ tag: 'js' }`
- `@Body('tag')` => `'js'`
- `@Query()` => `{ name: 'ninja' }`
- `@Query('name')` => `'ninja'`
- `@Headers()` => `{ ..., token: 'Bearer Token' }`
- `@Headers('token')` => `'Bearer Token'`
