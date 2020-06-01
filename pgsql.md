## pgsql

psql -h <host> -p <port> -U <username> -W <password> <database>

psql -h  apd4-bi-tdw -p 5432 -U clientspeeddata -W speeddata123 teg_apd_expeva4


查看所有数据库 \l

使用某个数据库 \c dbname 