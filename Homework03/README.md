#### Postgres16 установлен локально на Deb12
```
● postgresql.service - PostgreSQL RDBMS
     Loaded: loaded (/lib/systemd/system/postgresql.service; enabled; preset: enabled)
     Active: active (exited) since Mon 2024-09-23 19:01:16 MSK; 37min ago
   Main PID: 925 (code=exited, status=0/SUCCESS)
        CPU: 935us

Warning: some journal files were not opened due to insufficient permissions.
```
#### Подключился локально к базе и создал тестовую базу и пользователя
```
sudo -u postgres psql
CREATE USER kkorshunov WITH PASSWORD '12345678';
CREATE DATABASE homework_03 OWNER kkorshunov;
\c homework_03;
```



#### Зашел в базу под новым пользователем и создал таблицу
```
root@kkorshunov:/home/kkorshunov# psql dbname=homework_03 -U kkorshunov
Password for user kkorshunov: 
psql (16.4 (Debian 16.4-1.pgdg120+1))
Type "help" for help.

CREATE TABLE public.test_table (
        name varchar NULL,
        surname varchar NULL,
        id int GENERATED ALWAYS AS IDENTITY NOT NULL,
        CONSTRAINT test_table_pk PRIMARY KEY (id)
);


homework_03=> \dt
            List of relations
 Schema |    Name    | Type  |   Owner    
--------+------------+-------+------------
 public | test_table | table | kkorshunov
(1 row)

homework_03=> \q
```

#### Общий список баз 
```
root@kkorshunov:/home/kkorshunov# sudo -u postgres psql
psql (16.4 (Debian 16.4-1.pgdg120+1))
Type "help" for help.

postgres=# \l
                                                         List of databases
    Name     |   Owner    | Encoding | Locale Provider |   Collate   |    Ctype    | ICU Locale | ICU Rules |   Access privileges   
-------------+------------+----------+-----------------+-------------+-------------+------------+-----------+-----------------------
 homework_03 | kkorshunov | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | 
 postgres    | postgres   | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | 
 template0   | postgres   | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | =c/postgres          +
             |            |          |                 |             |             |            |           | postgres=CTc/postgres
 template1   | postgres   | UTF8     | libc            | en_US.UTF-8 | en_US.UTF-8 |            |           | =c/postgres          +
             |            |          |                 |             |             |            |           | postgres=CTc/postgres
(4 rows)

postgres=# \q
```

#### Подключился к базе DBeaver'om под новым пользователем 
скрин во вложении, все ок
