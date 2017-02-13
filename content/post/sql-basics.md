+++
date = "2017-02-12T18:56:33-05:00"
title = "sql basics"

+++

## select

`select` fields `from` a table.

select all fields:

```sql
select
    *
from
    customers
```

select specific fields:

```sql
select
    name,
    species
from
    pets
```

## where

the `where` clause is used for filtering data.

get all gerbils:

```sql
select
    *
from
    pets
where
    species = 'gerbil'
```

get all gerbils that are older than 5:

```sql
select
    *
from
    pets
where
    species = 'gerbil'
    and
    age > 5
```

get all pets that are either a gerbil or a dog:

```sql
select
    *
from
    pets
where
    species = 'gerbil'
    or
    species = 'dog'
```

## sum(), count(), and group by

aggregate data using an aggregate function like `sum()` or `count()` in combination with the `group by` clause.

count number of each species:

```sql
select
    species,
    count(*)
from
    pets
group by
    species
```

get total quantity sold of each `item_id` from all transactions:

```sql
select
    item_id,
    sum(quantity)
from
    transaction_items
group by
    item_id
```

## order by

sort your results.

sort customer names:

```sql
select
    first,
    last
from
    customers
order by
    last
```

sort items by price:

```sql
select
    name,
    price
from
    items
order by
    price desc
```

## limit

`limit` the amount of results you return.

```sql
select
    *
from
    customers
limit
    5
```

## as

alias your field names `as` a more descriptive name.

```sql
select
    first as first_name,
    last as last_name
from
    customers
```

## joins

the meat of SQL. `join` data from one table to another `on` a certain condition. specifically, we'll use `inner join`s for now. you can `join` multiple tables together by repeating the clause.

note the need to preface field names with the table they belong to.

```sql
select
    customers.first,
    customers.last,
    pets.species,
    pets.name
from
    customers
inner join
    pets
    on
    customers.id = pets.owner_id
```

## putting it all together!

here's a mega query that uses all of the above concepts.

**give a summary of the first 8 transactions Queen Bey made at the pet store since 2010**

```sql
select
	transactions.date as transaction_date,
	sum(items.price) as total_cost,
	count(*) as number_of_items
from 
	transactions
inner join
	customers
	on
	customers.id = transactions.customer_id
inner join
	transaction_items
	on
	transactions.id = transaction_items.transaction_id
inner join
	items
	on
	items.id = transaction_items.item_id
where
	transactions.date >= '2010-01-01'
	and
	customers.first = 'beyonce'
group by
	transactions.date
order by
	transactions.date
limit
	8
```

## additional resources

[w3schools](http://www.w3schools.com/sql/sql_select.asp)
