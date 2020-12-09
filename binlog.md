``` 
mysqlbinlog --database=finance --skip-gtids=true mysql-bin.002159 mysql-bin.002160 mysql-bin.002161  mysql-bin.002162 mysql-bin.002163  mysql-bin.002164 mysql-bin.002165  mysql-bin.002166 |mysql -uroot -f -v finance  -p 
```