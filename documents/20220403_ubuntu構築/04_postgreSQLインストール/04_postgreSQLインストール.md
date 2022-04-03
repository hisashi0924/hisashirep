# postgreSQLインストール

作成日：2022-04-03

作成者：石田　和希

------

[TOC]

------





### 1.インストール

```bash
#  whoami
root


`インストール
# apt -y install postgresql-12 



`待ち受けアドレス設定
# vi /etc/postgresql/12/main/postgresql.conf 
-----------------------------------------------------------------------------------------------------
##### 2022-04-03 ADD start (hisashi)
listen_addresses = '*'
#### 2022-04-03 ADD end (hisashi)
-----------------------------------------------------------------------------------------------------


`接続元許可設定
# vi /etc/postgresql/12/main/pg_hba.conf
-----------------------------------------------------------------------------------------------------
# DO NOT DISABLE!
# If you change this first entry you will need to make sure that the
# database superuser can access the database using some other method.
# Noninteractive access to all databases is required during automatic
# maintenance (custom daily cronjobs, replication, and similar tasks).
#
# Database administrative login by Unix domain socket
local   all             postgres                                peer

# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     peer
# IPv4 local connections:
host    all             all             127.0.0.1/32            md5
host    all             all             10.90.211.0/24          md5	<--追加
# IPv6 local connections:
host    all             all             ::1/128                 md5
# Allow replication connections from localhost, by a user with the
# replication privilege.
local   replication     all                                     peer
host    replication     all             127.0.0.1/32            md5
host    replication     all             ::1/128                 md5
                                                                                             
-----------------------------------------------------------------------------------------------------


`サービス再起動
# systemctl restart postgresql


`postgresユーザへスイッチ
# su - postgres
$

$whoami
postgres

`postgres用ユーザ作成
$ createuser hisashi
$


`DB作成
$ createdb hisashidb -O hisashi
$


`ユーザの確認
$ psql -c "select usename from pg_user;"
 usename
----------
 postgres
 hisashi
(2 rows)


`DBの確認
$ psql -l
                                  List of databases
   Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges
-----------+----------+----------+-------------+-------------+-----------------------
 hisashidb | hisashi  | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 postgres  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 template0 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
(4 rows)


`postgresターミナルにログイン
$ psql

`postgresユーザのパスワードの設定
=# alter role postgres with password 'pgsql-001';
ALTER ROLE

`hisashiユーザのパスワードの設定
=# alter role hisashi with password 'hisashi-001';
ALTER ROLE

`ログアウト
=# \q


`ufwの調整
# ufw allow in on ens160 to any port postgres
Rule added


`dbに接続できることを確認する
```




