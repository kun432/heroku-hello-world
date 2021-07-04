# heroku-hello-world

heroku練習用

以下を参考にさせてもらっった
https://gist.github.com/9sako6/50fbb501ccd64b2b77c1fe2b00086b71

## nodeアプリ作成

```sh
$ mkdir heroku-hello-world
$ npm init # 適当に
$ npm install express -save
```

index.js作成

```js
const express = require('express');
const app = express();

app.set('port', (process.env.PORT || 3000));

app.get('/', function(request, response) {
  response.send('Hello World!\n');
});

app.listen(app.get('port'), function() {
  console.log("Node app is running at localhost:" + app.get('port'));
});
```

テストする

```sh
$ node index.js
Node app is running at localhost:3000
```

```
$ curl localhost:3000
Hello World!
```

確認できたらCtrl+Cで止める

## herokuデプロイ

まずgitで初期化

```
$ git init
$ gibo dump macOS Node > .gitignore
```

Procfileを作成

```
web: node index.js
```

herokuにログイン、適当にキーを叩くとブラウザでログイン画面が出る

```
$ heroku login
heroku: Press any key to open up the browser to login or q to exit: 
```

ログインが成功したらターミナルに戻って、ログイン済みになっていることを確認。

```
Logging in... done
Logged in as foobar@example.com
```

herokuにpushする

```
$ git add .
$ git commit -m "initial commit"
$ heroku create
$ git push heroku master
$ heroku open
```

