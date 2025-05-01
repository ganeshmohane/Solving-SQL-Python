**Q.1 Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.**
```sql
select patient_id,first_name
from patients
where first_name like 's____%s'
```

**Q.2 Show the ProductName, CompanyName, CategoryName from the products, suppliers, and categories table.**
```sql
select p.product_name, c.category_name, s.company_name
from products p 
left join categories c on p.category_id = c.category_id
left join suppliers s on p.supplier_id = s.supplier_id
```

**Q.3 Show the category_name and the average product unit price for each category rounded to 2 decimal places.**
```sql
select c.category_name, round(avg(p.unit_price),2) as average_unit_price
from products p 
left join categories c on p.category_id = c.category_id
group by category_name
```

**Q.4 We want to display each patient's full name in a single column. Their last_name in all upper letters must appear first, then first_name in all lower case letters. Separate the last_name and first_name with a comma. Order the list by the first_name in decending order
EX: SMITH,jane**
```sql
select concat(upper(last_name),',', lower(first_name)) as new_name_format
from patients
order by first_name desc
```

**Q.5 Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'. Primary diagnosis is stored in the admissions table.**
```sql
select patient_id, first_name, last_name
from patients
where patient_id In 
(select patient_id from admissions
where diagnosis = 'Dementia')
```