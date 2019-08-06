# 詰まったことメモ

## PHP5.3→7.3

- `mysql_xx()`メソッドは、①プリペアードステートメントに非対応だったり、②MySQLの全機能に対応していないなどの理由により廃止されている。`mysqli_xx()`メソッド、または、PDOを使うべし。
- 



## Docker

- Dockerfileに `RUN docker-php-ext-install pdo_mysql mysqli mbstring`を書く必要がある。
- 上記のようにDockerfileに修正を加えた場合は、`--build`をつけてコンテナを作り直す必要がある。でないと、修正が適用されない。
- 
