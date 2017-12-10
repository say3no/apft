# 自分の開発環境について

## SDKについて
2017/12/10現在、WordPressのSDKはcomposerで配布されていない。
開発に最低限必用なものは`wordpress`,`wordpress-test-lib`,そしてこいつの親クラスである`phpunit`の３つだ。
`phpunit`は`composer install`で持ってくるとして、WordPress関係のものは公式が作成したスクリプト(同梱してある)`bin/install-wp-tests.sh`でpullできる。

```
bin/install-wp-tests.sh wp_test wp_test 'wp_test' localhost latest 
```

このシェルは、シェル内で定義された`install_wp`,`install_test_suite`,`install_db`の３つの関数を順に実行するというもので、
mysqldが建っていないと`install_db`が失敗するが、必用なのは始めの２つで十分なので問題ない。
成功すると、`/tmp/wordpress`,`/tmp/wordpress-tests-lib`に生成される。なお`/tmp`下なので多くの場合再起動すると消える。
このパッケージへのパスは`tests/bootstrap.php`で定義されているのだが、
それはそれとして、私は開発に必用なものは全てリポジトリ下のディレクトリに格納したいので、

```
cp -r /tmp/wordpress vendor/.
cp -r /tmp/wordpress-tests-lib vendor/.
```
としている。

## 動作確認
実際にブラウザで目視テストをする場合、`docker-compose up`で`localhost:8080`でアクセスできる。
この`docker-compose.yml`はwordpress公式のdocker-hubからコピペしてきたものに、
1. このプラグインをバインド
2. mysqldが全クエリのログを取るような`conf.d`のバインド
という一手間をくわえたものだ。

私はWordpressのプロセスがどうなっているのか詳しく無い為、ドキュメントとは別にクエリの流れを見たい事があるので、
大体、`docker-compose up`した後に、別のターミナルから
```
docker exec -ti [__NAME__]_mysql_1 /bin/bash
tail -f /var/log/mysql/general.log
```
をしている。


## 開発の流れ
今回、@yousanのadd-page-from-templateというプラグインをTDDでクローンをするという目的で動いている。

### ActivateするとSettingsのところにページリンクが追加される


#### pluginの基本





