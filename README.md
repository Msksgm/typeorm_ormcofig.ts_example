# typeorm_ormcofig.ts_example

## 概要

tsconfig.ts を読み込むサンプルアプリです．  
詳しくは[こちらの記事]()を参照

## 準備

### docker compose

docker compose で DB サーバーを起動

```sh
sh docker compose up -d
```

`typeorm_ormconfig.ts_example/.env`ファイルを作成

```text
# DB
DB_HOST=127.0.0.1
DB_PORT=13306
DB_USERNAME=root
DB_PASSWORD=password
DB_DATABASE=typeorm_db
```

環境変数を読み込む

```text
export $(cat .env | grep -v ^# | xargs)
```

## 動作確認

### migration

`migration:generate`

```sh
npx ts-node ./node_modules/.bin/typeorm migration:generate -n user -f ./src/config/ormconfig.ts
```

`migration:run`

```sh
npx ts-node ./node_modules/.bin/typeorm migration:run -f ./src/config/ormconfig.ts
```

### MySQL を確認

```sh
mysql -u root --port 13306 -h 127.0.0.1 -D typeorm_db -e 'SELECT * FROM user;' -p
```

出力

```sh
+----+-----------+----------+-----+
| id | firstName | lastName | age |
+----+-----------+----------+-----+
|  1 | Timber    | Saw      |  25 |
+----+-----------+----------+-----+
```
