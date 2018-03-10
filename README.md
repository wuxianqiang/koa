# koa

```js
const Koa = require('koa')
const app = new Koa()
app.listen(8080, () => {
  console.log('port in 8080!')
})
```
使用koa搭建web服务比使用express简单得多。koa支持`async/awit`语法，所以可以明显减少回调嵌套。

## 接收GET数据
```js
const Koa = require('koa')
const app = new Koa()

app.use(async (ctx, next) => {
  let GET = ctx.query
  console.log(GET)
  ctx.body = 'ok'
})

app.listen(8080, () => {
  console.log('port in 8080!')
})

```
## 处理路由
```js
const Koa = require('koa')
const Router = require('koa-router')
const app = new Koa()

//https://xxx.com/user/1.html
//https://xxx.com/user/2.html
const router = new Router()
const routerUser = new Router()

routerUser.get("/1.html", async (ctx, next) {
  ctx.body("1")
})
routerUser.get("/2.html", async (ctx, next) {
  ctx.body("2")
})

app.use(router.routes())
app.use(router.allowedMethods())

router.use('/user', routerUser.routes())
router.use('/user', routerUser.allowedMethods())

app.listen(8080, () => {
  console.log('port in 8080!')
})
```
## 处理文件
