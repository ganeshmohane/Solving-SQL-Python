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

**Q.6 All patients who have gone through admissions, can see their medical documents on our site. Those patients are given a temporary password after their first admission. Show the patient_id and temp_password.**

The password must be the following, in order:
1. patient_id
2. the numerical length of patient's last_name
3. year of patient's birth_date
```sql
select distinct p.patient_id, concat(p.patient_id, len(p.last_name), year(p.birth_date)) as temp_password
from patients p 
join admissions a on p.patient_id = a.patient_id
```

**Q.7 Display every patient's first_name. Order the list by the length of each name and then by alphabetically.**
```sql
select first_name
from patients
order by len(first_name), first_name asc
```
**Q.8 Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.**
```sql
select patient_id, diagnosis
from admissions
group by diagnosis, patient_id
having count(*)>1
```
**Q.9 Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.**
```sql
select province_id, sum(height) as sum_height
from patients
Group by province_id
having sum_height>=7000
```
**Q.10 Show the difference between the largest weight and smallest weight for patients with the last name 'Maroni'**
```sql
select (Max(weight)-min(weight)) as weight_difference
from patients
where last_name = 'Maroni'
```
**Q.11 Show all of the days of the month (1-31) and how many admission_dates occurred on that day. Sort by the day with most admissions to least admissions.**
```sql
select day(admission_date) as day_number, count(patient_id) as number_of_admissions
from admissions
group by day_number
order by number_of_admissions desc
```
**Q.12 Show the city and the total number of patients in the city. Order from most to least patients and then by city name ascending.**
```sql
select city, count(*) as num_patients
from patients
group by city
order by num_patients desc, city
```
**Q.13 Show all columns for patient_id 542's most recent admission_date.**
```sql
select * 
from admissions
where patient_id = 542
order by admission_date desc
limit 1
```
**Q.14 Show patient_id, attending_doctor_id, and diagnosis for admissions that match one of the two criteria:**
1. patient_id is an odd number and attending_doctor_id is either 1, 5, or 19.
2. attending_doctor_id contains a 2 and the length of patient_id is 3 characters.
```sql
select patient_id, attending_doctor_id, diagnosis
from admissions
where ((patient_id % 2 != 0) and (attending_doctor_id in (1,5,19))) or ((attending_doctor_id like '%2%')  and (length(patient_id)=3))
```
**Q.15 Show unique birth years from patients and order them by ascending.**
```sql
select distinct year(birth_date) as birth_year
from patients
order by birth_year asc
```
**Q.16 Display the total amount of patients for each province. Order by descending.**
```sql
select pv.province_name as province_name, count(pt.patient_id) as patient_count
from patients pt
join province_names pv on pt.province_id = pv.province_id
group by province_name
order by patient_count desc
```
**Q.17 Show first name, last name and role of every person that is either patient or doctor.
The roles are either "Patient" or "Doctor"**
```sql
select first_name, last_name, 'Patient' as role
from patients
union all
select first_name, last_name, 'Doctor' as role
from doctors
```
**Q.18 Show all allergies ordered by popularity. Remove NULL values from query.**
```sql
select allergies, count(*) as total_diagnosis
from patients
where allergies not null
group by allergies
order by total_diagnosis desc
```
**Q.19 Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date.**
```sql
select first_name, last_name, birth_date
from patients
where year(birth_date) between 1970 and 1979
order by birth_date asc
```
**Q.20 For each doctor, display their id, full name, and the first and last admission date they attended.**
```sql
select doctor_id, 
concat(first_name,' ', last_name) as full_name,
min(admission_date) as first_admission_date, max(admission_date) as last_admission_date
from doctors doc
join admissions adm on doc.doctor_id = adm.attending_doctor_id
group by doctor_id
order by doctor_id
```
