# pt-query-digestの使い方

MySQLのクエリログを解析するためのツール。

## インストール

Macの場合はHomebrewでインストールできる。

```bash
brew install percona-toolkit
```

## MySQLのスロークエリログをオンにする

ISUCONのときは、`long_query_time`を`0`にすると強い人が言っていたのでそうする。

MySQLの変数と設定ファイルのセクションについて前ちょっと調べたのでまとめたい。

```bash
# ローカルのMySQLを使っていたため、直接サーバーシステム変数を書き換えている
mysql> show variables like '%slow%';
+---------------------------+---------------------------------------+
| Variable_name             | Value                                 |
+---------------------------+---------------------------------------+
| log_slow_admin_statements | OFF                                   |
| log_slow_extra            | OFF                                   |
| log_slow_slave_statements | OFF                                   |
| slow_launch_time          | 2                                     |
| slow_query_log            | OFF                                   |
| slow_query_log_file       | /usr/local/var/mysql/gib0017-slow.log |
+---------------------------+---------------------------------------+
6 rows in set (0.13 sec)

mysql> show variables like '%long%';
+----------------------------------------------------------+-----------+
| Variable_name                                            | Value     |
+----------------------------------------------------------+-----------+
| long_query_time                                          | 10.000000 |
| performance_schema_events_stages_history_long_size       | 10000     |
| performance_schema_events_statements_history_long_size   | 10000     |
| performance_schema_events_transactions_history_long_size | 10000     |
| performance_schema_events_waits_history_long_size        | 10000     |
+----------------------------------------------------------+-----------+
5 rows in set (0.03 sec)

mysql> set global long_query_time=0;
Query OK, 0 rows affected (0.02 sec)

mysql> set global slow_query_log=1;
Query OK, 0 rows affected (0.09 sec)
```

## クエリを解析する

```bash
pt-query-digest --limit 5 [クエリログのファイル]
```

上のセクションにはクエリ全体の解析結果のまとめが書かれてある。
その下には、各クエリについての解析結果の詳細が書かれてある。

## 参考

- [Percona Toolkitをインストールし、pt-query-digestでスロークエリログを解析する手順 | Enjoy IT Life](https://nishinatoshiharu.com/percona-slowquerylog/)
