**Q.1 Show patient_id, first_name, last_name, and attending doctor's specialty.
Show only the patients who has a diagnosis as 'Epilepsy' and the doctor's first name is 'Lisa'
Check patients, admissions, and doctors tables for required information.**
```sql
select pt.patient_id, pt.first_name, pt.last_name, doc.specialty
from patients pt
join admissions ad on pt.patient_id = ad.patient_id
join doctors doc on ad.attending_doctor_id = doc.doctor_id
where ad.diagnosis = 'Epilepsy' and doc.first_name = 'Lisa'
```
