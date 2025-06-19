create a user and grant all the privileges to them:

```sql
CREATE USER 'username'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'username'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

Open the database to access anywhere:

go to `/etc/mysql/mysql.conf.d/` then edit `mysqld.cnf`

change the `bind-address` to `0.0.0.0`


