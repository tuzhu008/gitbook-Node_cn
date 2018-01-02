# Formidable

[![Build Status](https://travis-ci.org/felixge/node-formidable.svg?branch=master)](https://travis-ci.org/felixge/node-formidable)

## 用途

一个 Node.js 模块，用于解析表单数据，尤其是文件上传。

## 当前状态

**诚寻维护者:** 请参见 https://github.com/felixge/node-formidable/issues/412

此模块是为 [Transloadit](http://transloadit.com/) 开发的，该服务专注于上传
并编码图像和视频。它已经久经沙场，已处理了数百 GB 的来自各种客户端的文件上传，并被认为是可量产的。

## 特性

* 快速 (~500mb/sec), 非缓冲多部分解析器
* 自动将文件上传到磁盘
* 低内存占用
* 优雅的错误处理
* 非常高的测试覆盖率

## 安装

```sh
npm i -S formidable
```
这是一个低阶的包，如果你使用的是一个高阶的框架，它可能已经被包含在内了。然而 [Express v4](http://expressjs.com)  没有包含任何多部分（multipart）处理，也没有 [body-parser](https://github.com/expressjs/body-parser)。

注意: Formidable 需要 [gently](http://github.com/felixge/node-gently) 来运行单元测试，但是你不需要它，只管使用这个库。

## 示例

解析传入的文件上传。

```javascript
var formidable = require('formidable'),
    http = require('http'),
    util = require('util');

http.createServer(function(req, res) {
  if (req.url == '/upload' && req.method.toLowerCase() == 'post') {
    // parse a file upload
    var form = new formidable.IncomingForm();

    form.parse(req, function(err, fields, files) {
      res.writeHead(200, {'content-type': 'text/plain'});
      res.write('received upload:\n\n');
      res.end(util.inspect({fields: fields, files: files}));
    });

    return;
  }

  // 显示一个文件上传表单
  res.writeHead(200, {'content-type': 'text/html'});
  res.end(
    '<form action="/upload" enctype="multipart/form-data" method="post">'+
    '<input type="text" name="title"><br>'+
    '<input type="file" name="upload" multiple="multiple"><br>'+
    '<input type="submit" value="Upload">'+
    '</form>'
  );
}).listen(8080);
```
## API

### Formidable.IncomingForm

```javascript
var form = new formidable.IncomingForm()
```
创建一个新的传入表单。

> **[info] 「译者注：」**
>
> 表单具有如下属性：
> 
>         属性           |        描述
> ----------------------|--------------------
>     `encoding`        |  为传入表单的字段设置字符编码
>     `uploadDir`       |  设置放置文件的目录
>     `keepExtensions`  |  如果你想要写入 `form.uploadDir` 的文件包含原始文件的扩展名，设置这个属性为`true`
>     `type`            |  根据传入的请求，可以是 'multipart' 或 'urlencoded'
>     `maxFieldsSize`   |   限制所有字段的内存量
>     `maxFields`       |   限制将被解码查询字符串解析器的字段数。 
>     `hash`            |   如果你想为传入的文件计算校验和，把它设置为 'sha1' 或 'md5'。
>     `multiples`       |   启用多文件上传
>     `bytesReceived`   |   到目前为止，这个表单收到的字节数量。
>     `bytesExpected`   |   这个表单的预期字节数。
>     `parse()`         |   解析一个传入的 node.js `request`
>     `onPart()`        |
>     `handlePart()`    |


```javascript
form.encoding = 'utf-8';
```
为传入表单的字段设置字符编码。

```javascript
form.uploadDir = "/my/dir";
```
设置放置文件的目录。您可以稍后使用 `fs.rename()` 移动它们。 默认是[`os.tmpdir()`](http://nodejs.cn/api/os.html#os_os_tmpdir)。

```javascript
form.keepExtensions = false;
```
如果你想要写入 `form.uploadDir` 的文件包含原始文件的扩展名，设置这个属性为`true`。

```javascript
form.type
```
根据传入的请求，可以是 'multipart' 或 'urlencoded'。

```javascript
form.maxFieldsSize = 2 * 1024 * 1024;
```
限制所有字段的内存量（文件除外）可以按字节分配。如果超过这个值，则会发出 `'error'` 事件。默认大小是 2MB。

```javascript
form.maxFields = 1000;
```

限制将被解码查询字符串解析器的字段数。 默认为 1000（无限制为 0）。

```javascript
form.hash = false;
```
如果你想为传入的文件计算校验和，把它设置为 `'sha1'` 或 `'md5'`。

```javascript
form.multiples = false;
```
如果这个选项被启用，当调用 `form.parse` 时，`files` 参数将包含输入框文件的数组，这个输入框使用 HTML5 `multiple` 属性提交多个文件。

```javascript
form.bytesReceived
```
到目前为止，这个表单收到的字节数量。

```javascript
form.bytesExpected
```
这个表单的预期字节数。

```javascript
form.parse(request, [cb]);
```

解析一个传入的 node.js `request`，它包含表单数据。如果提供了 `cb`，所有字段和文件都被收集起来并传递给回调：

```javascript
form.parse(req, function(err, fields, files) {
  // ...
});

form.onPart(part);
```

如果您有兴趣直接访问多部分流，则可以重写此方法。这样做会禁用所有将会发生的 `'field'` / `'file'` 事件处理，使您全权处理。

```javascript
form.onPart = function(part) {
  part.addListener('data', function() {
    // ...
  });
}
```

如果你想使用 formidable 来处理某些部分，你可以这样做：

```javascript
form.onPart = function(part) {
  if (!part.filename) {
    // let formidable handle all non-file parts
    form.handlePart(part);
  }
}
```
检查此方法中的代码以获取更多灵感。


### Formidable.File

> **[info] 「译者注：」**
>
> 文件有如下属性：
>
> 属性           |        描述
> ----------------------|--------------------
>       `size`          |  上传文件的大小（以字节为单位）。
>       `path`          |  该文件正在被写入的路径
>       `name`          |  这个文件的名字是根据上传客户端来的。
>       `type`          |  该文件的MIME类型，根据上> 传客户端。 的文件包含原始文件的扩展名，设置这个属性为`true`
>   `lastModifiedDate`  |  一个日期对象（或 null）,包含上次写入该文件的时间。
>       `hash`          |   如果设置了哈希计算，则可以从该变量中读取十六进制摘要。
>       `toJSON()`      |   此方法返回文件的 JSON 表示形式

```javascript
file.size = 0
```

上传文件的大小（以字节为单位）。 如果文件仍然在上传（参见 `fileBegin'` 事件），这个属性说明文件有多少个字节已经被写入磁盘了。



```javascript
file.path = null
```

该文件正在被写入的路径。你可以在 `'fileBegin'` 事件中修改这个事件，以防你不满意的这种方式，formidable 为你的文件生成一个临时路径。

```javascript
file.name = null
```

这个文件的名字是根据上传客户端来的。

```javascript
file.type = null
```
该文件的MIME类型，根据上传客户端。

```javascript
file.lastModifiedDate = null
```

一个日期对象（或 `null`）,包含上次写入该文件的时间。 主要是为了与[W3C File API 草案](http://dev.w3.org/2006/webapi/FileAPI/) 兼容。

```javascript
file.hash = null
```

如果设置了哈希计算，则可以从该变量中读取十六进制摘要。

#### Formidable.File#toJSON()


  此方法返回文件的 JSON 表示形式，允许您使用 `JSON.stringify()` 该文件，这对于记录和响应请求很有用。

### 事件

> **[info] 「译者注：」**
>
> 事件列表
>
>       事件名    |         描述
> ---------------|------------------
>    'progress'  |  在每个传入的数据块已经被解析后被发射。
>    'field'     |  每当收到一个 字段/值 对时被发射。
>    'fileBegin' |  在上传流中检测到新文件时被发射。
>    'file'      |  每当接收到一个 字段/文件 对时被发发射。
>    'error'     |  在处理传入表单发生错误时被发射
>    'aborted'   |  当请求被用户中止时被发射。
>    'end'       |  当收到整个请求时被发射

#### 'progress'

在每个传入的数据块已经被解析后被发射。可以用来滚动你自己的进度条。

```javascript
form.on('progress', function(bytesReceived, bytesExpected) {
});
```

#### 'field'

每当收到一个 字段/值 对时被发射。

```javascript
form.on('field', function(name, value) {
});
```

#### 'fileBegin'

在上传流中检测到新文件时被发射。如果要将文件流式传输到其他位置，同时缓冲文件系统上的上传，请使用此事件。

```javascript
form.on('fileBegin', function(name, file) {
});
```

#### 'file'

每当接收到一个 字段/文件 对时被发发射。 `file` 是 `File` 的一个实例。

```javascript
form.on('file', function(name, file) {
});
```

#### 'error'

在处理传入表单发生错误时被发射。遇到错误，请求会自动暂停，如果您希望请求继续触发 `'data'` 事件，则必须手动调用 `request.resume()`。

```javascript
form.on('error', function(err) {
});
```

#### 'aborted'

当请求被用户中止时被发射。现在这可能是由于套接字上的 'timeout' 或 'close' 事件。在这个事件被发射之后，将会跟随一个 `error` 事件。将来会有一个单独的 'timeout' 事件（需要在 node 核心中进行更改）。

```javascript
form.on('aborted', function() {
});
```

##### 'end'
```javascript
form.on('end', function() {
});
```

当收到整个请求时被发射，所有包含的文件已经完成冲洗（flushing）到磁盘。 这是您发送响应的好地方。


## 更新日志

### v1.1.1 (2017-01-15)

 * Fix DeprecationWarning about os.tmpDir() (Christian)
 * Update `buffer.write` order of arguments for Node 7 (Kornel Lesiński)
 * JSON Parser emits error events to the IncomingForm (alessio.montagnani)
 * Improved Content-Disposition parsing (Sebastien)
 * Access WriteStream of fs during runtime instead of include time (Jonas Amundsen)
 * Use built-in toString to convert buffer to hex (Charmander)
 * Add hash to json if present (Nick Stamas)
 * Add license to package.json (Simen Bekkhus)

### v1.0.14 (2013-05-03)

* Add failing hash tests. (Ben Trask)
* Enable hash calculation again (Eugene Girshov)
* Test for immediate data events (Tim Smart)
* Re-arrange IncomingForm#parse (Tim Smart)

### v1.0.13

* Only update hash if update method exists (Sven Lito)
* According to travis v0.10 needs to go quoted (Sven Lito)
* Bumping build node versions (Sven Lito)
* Additional fix for empty requests (Eugene Girshov)
* Change the default to 1000, to match the new Node behaviour. (OrangeDog)
* Add ability to control maxKeys in the querystring parser. (OrangeDog)
* Adjust test case to work with node 0.9.x (Eugene Girshov)
* Update package.json (Sven Lito)
* Path adjustment according to eb4468b (Markus Ast)

### v1.0.12

* Emit error on aborted connections (Eugene Girshov)
* Add support for empty requests (Eugene Girshov)
* Fix name/filename handling in Content-Disposition (jesperp)
* Tolerate malformed closing boundary in multipart (Eugene Girshov)
* Ignore preamble in multipart messages (Eugene Girshov)
* Add support for application/json (Mike Frey, Carlos Rodriguez)
* Add support for Base64 encoding (Elmer Bulthuis)
* Add File#toJSON (TJ Holowaychuk)
* Remove support for Node.js 0.4 & 0.6 (Andrew Kelley)
* Documentation improvements (Sven Lito, Andre Azevedo)
* Add support for application/octet-stream (Ion Lupascu, Chris Scribner)
* Use os.tmpdir() to get tmp directory (Andrew Kelley)
* Improve package.json (Andrew Kelley, Sven Lito)
* Fix benchmark script (Andrew Kelley)
* Fix scope issue in incoming_forms (Sven Lito)
* Fix file handle leak on error (OrangeDog)

## License

Formidable is licensed under the MIT license.

## 移植

* [multipart-parser](http://github.com/FooBarWidget/multipart-parser): 基于 formidable 的 C++ 解析器。

## 关于作者

* [Ryan Dahl](http://twitter.com/ryah) 在 [http-parser](http://github.com/ry/http-parser) 方面的工作深深地激发了 multipart_parser.js
