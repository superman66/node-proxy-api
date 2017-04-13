# Node + Express + superagent 转发 API 请求
简单的几行代码实现如何通过Node + Express + superagent 转发 API 请求。已部署到 Heroku。

**安装依赖**

Node.js 转发请求用到了 `express`和`superagent`. [superanget](https://github.com/visionmedia/superagent)是一个 Node.js HTTP client。
```
npm install express superagent --save
```

**端口设置**

由于部署到Heroku时，端口是动态分配的，所以需要根据 `process.env.NODE_ENV` 动态设置端口:
```javascript
app.set('port', (process.env.PORT || 5000));
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
app.listen(app.get('port'), function() {
  console.log('Node app is running on port', app.get('port'));
});
```
**启动**

```
cd node-proxy
node index.js
```

具体见`node-proxy/index.js`

# 部署到Heroku
详情见： [官方 Getting Started](https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction)
