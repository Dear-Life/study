### 文件系统

```javascript
fs.writeFile("a.txt", "秋瓷炫", function (err) {
  if (err) {
    console.log("error");
  }
});

fs.writeFileSync("a.txt", "111", { flag: "a" });

const ws = fs.createWriteStream("a.txt");
ws.on("open", function () {
  console.log("open");
});
ws.on("close", function () {
  console.log("close");
});
ws.write("A");
ws.write("B");
ws.close();
```

```javascript
fs.readFile("a.txt", function (err, data) {
  if (err) {
    console.log(err);
  } else {
    console.log(data.toString());
  }
});

const data = fs.readFileSync("a.txt");
console.log(data.toString());

const rs = fs.createReadStream("a.txt");
var ret = "";
rs.on("data", function (chunk) {
  ret += chunk.toString();
});
rs.on("close", function () {
  console.log(ret);
});
```

### 文件复制

```javascript
const rs = fs.createReadStream("a.txt");
const ws = fs.createWriteStream("b.txt");
rs.on("data", function (chunk) {
  ws.write(chunk);
});
rs.on("close", function () {
  ws.close();
});

const rs = fs.createReadStream("a.txt");
const ws = fs.createWriteStream("b.txt");
rs.pipe(ws);
```

### 文件其他操作

```javascript
fs.rename("aa.txt", "cc.txt", (err) => {
  if (err) throw err;
  console.log("Rename complete!");
});

fs.unlink("cc.txt", (err) => {
  if (err) throw err;
  console.log("deleted");
});

fs.mkdir("public", (error) => {
  if (error) {
    throw error;
  }
});

fs.readdir("./", (err, list) => {
  if (err) {
    throw error;
  }
  console.log(list);
});

fs.rmdir("public", (err) => {
  if (err) {
    throw err;
  }
});
```

### http 模块

```javascript
const http = require("http");
const fs = require("fs");
const url = require("url");
const { resolve } = require("path");

http
  .createServer(function (req, res) {
    if (req.url === "/favicon.ico") {
      return;
    }
    // console.log('method', req.method)
    // console.log('url', req.url)
    // console.log('httpVersion', req.httpVersion)
    // console.log('headers', req.headers)

    // GET 参数
    // console.log(url.parse(req.url, true).query)

    // POST 参数
    // if (req.method === "POST") {
    //     let data = ""
    //     req.on("data", function (chunk) {
    //         data += chunk
    //     })
    //     req.on("end", function () {
    //         console.log(new url.URLSearchParams(data))
    //     })
    // }

    // 响应处理
    // res.setHeader("name", "YISA")
    // text/plain
    // res.setHeader("content-type", "text/html")
    // res.statusCode = 404
    // res.end("hello world")

    // 静态资源
    let filePath = "public";
    if (req.url === "/") {
      filePath += "/index.html";
    } else {
      filePath += url.parse(req.url, true).pathname;
    }

    const data = fs.readFileSync(resolve(__dirname, filePath));
    res.write(data);
    res.end();
  })
  .listen(80);
```
