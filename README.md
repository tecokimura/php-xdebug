# php-xdebug

# これはなに？
PHPStormとXDebugでBreakpointを入れてデバッグをしたかったが全然設定がうまく行かなかったのでまっさらから初めて記録しておく

# 書き始めた日付
2020/07/03

# 使うもの
## XDebug
https://xdebug.org/

## OS X
version 0.15.5

## docker
docker-compose version 1.25.5, build 8a1c60f6
Docker version 19.03.8, build afacb8b

## PHPStorm

## VisualStudioCode

## Chrome



# localhost/index.html 

## docker
Dockerfile, php.ini はどなたかのサンプルを参考に作成
localhostでのindex.htmlのアクセスは成功

##### TODO
build時にWarnが出てるので動くが変な所ありそう

### docker-compose command
$ docker-compose build
$ docker-compose up

## PHP
php7.3-apache

## config
docker/php/php.ini

## RESULT
phpinfo(); 正常に表示

### xdebug動いてる？
https://xdebug.org/wizard
にphpinfo()の結果のソースを貼りボタンを押すとチェックしてくれる。

# 動いたのでPHPStormと連動

## PHPStorm
https://www.jetbrains.com/help/phpstorm/configuring-xdebug.html#integrationWithProduct

## Configure Xdebug in PhpStorm
PhpStorm でフォルダを開く
Settings/Preference > Languages & Frameworks > PHP

CLI Interpreter: docker-compose の php を指定する

Settings/Preference > Languages & Frameworks > PHP > Debug
Portの確認程度

## php.ini
xdebug.remote_enable=1
xdebug.remote_host=host.docker.internal
を足す

https://www.jetbrains.com/help/phpstorm/validating-the-configuration-of-the-debugging-engine.html#troubleshooting-validation-results
の検証をやってみる

PHPStormMenu > Run > Web Server Debug Validation
Path to create validation script にドキュメントルート(publicフォルダ)を指定する
Url to validation script: http:/localhost/

debug protocol '' is not supported phpstorm
だけエラーが出たが無視して良さそう

## Brower Debug extension
使っている（Chrome）ものをインストール

## Server
Settings/Preference > Languages & Frameworks > PHP > Server
+
Name:local-docker
Host:localhost
Port:80
Debugger:Xdebug
Use path mappings はドキュメントルートを設定


Menu > Run > Edit Configuration
+ > PHP Web Page
Name: any
Server: local-docker
Start URL: /index.php
Browser: Chrome (DefaultがChromeのアイコンだったが見事にSafariが立上る）

Breakpoint で止まらない


