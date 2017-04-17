# Mysql

Login

``` bash
mysql -u root -p;
```

Import database

``` bash
mysql> mysql -u root -p [dbname] < [sqlname.sql];
```

Export database
``` bash
mysql> mysqldump -u root -p [dbname] > [sqlname.sql];
```

Create database

```bash
mysql> CREATE DATABASE [dbname] DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
```

Account, set a password, and grant access to the database
```bash
mysql> GRANT ALL ON [dbname].* TO '[dbusername]'@'localhost' IDENTIFIED BY '[dbuserpassword]';
mysql> FLUSH PRIVILEGES;
```

Delete database

```bash
mysql> DROP DATABASE [dbaname];
```

Exit

```bash
mysql> EXIT;
```
