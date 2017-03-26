+++
date = "2017-02-25T17:24:17-05:00"
title = "postgres row numbers"

+++

To get just one result given a particular filter, you can
use `row_number()`.

In this case, I want to see an example of `detail` for each
different `id` in the table:

```sql
select * from (
    select
        id,
        detail,
        row_number() over (partition by id) as row_num
    from
        my_table
) x where row_num = 1
```
