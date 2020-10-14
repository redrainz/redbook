## 1. Update用join而不是in
```sql
    
     UPDATE  t
        inner join  t1
        on t.no =t1.order_no
        SET t.status = 0
        WHERE
           t1.flag = 0
        
```

```sql
    
     UPDATE  t
        where order_no 
        in(
        select order_no from t1 
        where  t1.flag = 0
        )
        
```