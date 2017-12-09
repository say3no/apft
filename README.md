# つらぽよ

WordPressには専用のテストフレームワークがあるのだが、そのテストフレームワークがcomposerでアクセスできないし、っていうかwpのコアファイルにもcomposerでアクセスできないため、プラグインをいざ作ろうと思うと環境整備に工夫が必用になる。
（糞で固目息)

実際にブラウザで目視テストをする場合、`docker-compose up`で`localhost:8080`でアクセスできる。
この`docker-compose.yml`はwordpress公式のdocker-hubからコピペしてきたものに、このプラグインをバインドするというひと手間を加えたものだ。

wordpress本体とテストフレームワークは、`bin/install-wp-tests.sh`でpullできる。
```
bash bin/install-wp-tests.sh wp_test wp_test 'wp_test' localhost latest 
```
デフォルトのパスは`/tmp/wordpress`,`/tmp/wordpress-tests-lib`となっており、`tests/bootstrap.php`で定義されている。