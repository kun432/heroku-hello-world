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

herokuにpushする。まず、コミット。

```
$ git add .
$ git commit -m "initial commit"
```

heroku側にアプリを作成。アプリケーションのURLおよびgitのリモートレポジトリが発行される。

```
$ heroku create
Creating app... done, ⬢ foo-bar-hogehoge-12345
https://foo-bar-hogehoge-12345.herokuapp.com/ | https://git.heroku.com/foo-bar-hogehoge-12345.git
```

heroku appsで確認できる

```
$ heroku apps
=== foobar@example.com
foo-bar-hogehoge-12345

$ heroku info --app foo-bar-hogehoge-12345
=== foo-bar-hogehoge-12345
Auto Cert Mgmt: false
Dynos:          
Git URL:        https://git.heroku.com/foo-bar-hogehoge-12345.git
Owner:          foobar@example.com
Region:         us
Repo Size:      0 B
Slug Size:      0 B
Stack:          heroku-20
Web URL:        https://foo-bar-hogehoge-12345.herokuapp.com/
```

git remoteでリモートレポジトリが作成されていることも確認できる

```
$ git remote -v
heroku  https://git.heroku.com/foo-bar-hogehoge-12345.git (fetch)
heroku  https://git.heroku.com/foo-bar-hogehoge-12345.git (push)
```

pushする

```
$ git push heroku master
```

ビルドしているログなどが流れる。

```
Enumerating objects: 8, done.
Counting objects: 100% (8/8), done.
Delta compression using up to 8 threads
Compressing objects: 100% (7/7), done.
Writing objects: 100% (8/8), 6.66 KiB | 3.33 MiB/s, done.
Total 8 (delta 0), reused 0 (delta 0), pack-reused 0
remote: Compressing source files... done.
remote: Building source:
remote: 
remote: -----> Building on the Heroku-20 stack
remote: -----> Determining which buildpack to use for this app
remote: -----> Node.js app detected
remote:        
remote: -----> Creating runtime environment
remote:        
remote:        NPM_CONFIG_LOGLEVEL=error
remote:        NODE_VERBOSE=false
remote:        NODE_ENV=production
remote:        NODE_MODULES_CACHE=true
remote:        
remote: -----> Installing binaries
remote:        engines.node (package.json):  unspecified
remote:        engines.npm (package.json):   unspecified (use default)
remote:        
remote:        Resolving node version 14.x...
remote:        Downloading and installing node 14.17.2...
remote:        Using default npm version: 6.14.13
remote:        
remote: -----> Installing dependencies
remote:        Installing node modules
remote:        added 50 packages in 1.105s
remote:        
remote: -----> Build
remote:        
remote: -----> Caching build
remote:        - node_modules
remote:        
remote: -----> Pruning devDependencies
remote:        audited 50 packages in 0.74s
remote:        found 0 vulnerabilities
remote:        
remote:        
remote: -----> Build succeeded!
remote: -----> Discovering process types
remote:        Procfile declares types -> web
remote: 
remote: -----> Compressing...
remote:        Done: 33.1M
remote: -----> Launching...
remote:        Released v3
remote:        https://foo-bar-hogehoge-12345.herokuapp.com/ deployed to Heroku
remote: 
remote: Verifying deploy... done.
To https://git.heroku.com/foo-bar-hogehoge-12345.git
 * [new branch]      master -> master
```

アプリのURLにアクセスして動くことを確認

```
$ curl https://foo-bar-hogehoge-12345.herokuapp.com/ 
Hello World!
```







$ git push heroku master
$ heroku open
```

