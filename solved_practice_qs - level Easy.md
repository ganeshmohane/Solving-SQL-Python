**Q.1 Show the category_name and description from the categories table sorted by category_name.**
```sql
select category_name, description
from categories
order by category_name
```

**Q.2 Show all the contact_name, address, city of all customers which are not from 'Germany', 'Mexico', 'Spain'**
```sql
select contact_name, address, city
from customers
where country not in ('Germany', 'Mexico', 'Spain')
```