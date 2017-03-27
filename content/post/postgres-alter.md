+++
date = "2017-03-27T12:25:30-04:00"
title = "postgres alter"

+++

## move schema

```sql
alter table old_schema.my_table set schema new_schema;
```

## rename table

```sql
alter table my_table rename to new_table_name;
```

## rename column

```sql
alter table my_table rename column old_col to new_col;
```


