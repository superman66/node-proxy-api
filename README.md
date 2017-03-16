# Node + Express + superagent 转发API请求
简单的几行代码实现如何通过Node + Express + superagent 转发API请求。
**安装依赖**

Node.js转发用到了 `express`和`superagent`. [superanget](https://github.com/visionmedia/superagent)是一个 Node.js HTTP client。
```
npm i express superagent -S
```
**定义接口**
根据前端所需，定义了如下三个接口：
```javascript
app.get('/movie/:type', function (req, res) {
  var sreq = request.get(HOST + req.originalUrl)
  sreq.pipe(res);
  sreq.on('end', function (error, res) {
    console.log('end');
  });
})

app.get('/movie/subject/:id', function (req, res) {
  var sreq = request.get(HOST + req.originalUrl)
  sreq.pipe(res);
  sreq.on('end', function (error, res) {
    console.log('end');
  });
})

app.get('/movie/search', function (req, res) {
  var sreq = request.get(HOST + req.originalUrl)
  sreq.pipe(res);
  sreq.on('end', function (error, res) {
    console.log('end');
  });
})
```

**CORS设置**
>跨源资源共享 ( [CORS](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS) )机制让Web应用服务器能支持跨站访问控制，从而使得安全地进行跨站数据传输成为可能。
主要是通过设置`Access-Control-Allow-Origin: *`
```javascript
app.all('*', function (req, res, next) {
  if (!req.get('Origin')) return next();
  // use "*" here to accept any origin
  res.set('Access-Control-Allow-Origin', '*');
  res.set('Access-Control-Allow-Methods', 'GET');
  res.set('Access-Control-Allow-Headers', 'X-Requested-With, Content-Type');
  // res.set('Access-Control-Allow-Max-Age', 3600);
  if ('OPTIONS' == req.method) return res.send(200);
  next();
});
```
**端口监听**
```javascript
app.listen(8081, function () {
  console.log('HTTP Server is running in http://127.0.0.1:8081')
})
```
**启动**

```
cd node-proxy
node index.js
```

具体见`node-proxy/index.js`
