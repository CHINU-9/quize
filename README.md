# quize

https://claude.ai/share/862aa579-98e1-439a-bb6d-477c16a6d50b

https://claude.ai/share/22b89e2d-7880-49f1-ab04-f91e3df107af
---1 number 
select p.name as patient, p.address, ph.name as physician
from patient p
join physician ph
on p.pcp = ph.employeeID;

---2 number
select p.name as patientname, n.name as nurse, ph.name as 'name of the physician', a.examinationroom as roomno, a.starttime as appointmenttime
from appointment a
join patient p
on a.patient = p.ssn
join physician ph
on a.physician = ph.employeeid
left join nurse n
on a.prepnurse = n.employeeid
where a.starttime = '2008-04-25 10:00:00';

---3 number
select 
     ph.name as physician,
     count(a.appointmentid) as totalappointment
from physician ph
join appointment a 
   on ph.employeeid = a.physician
group by ph.name
having count(a.appointmentid) > 1;

---4 number
select 
     ph.employeeid as physicianid,
     ph.name as physicianname,
     u.proceduredate as proceduredate,
     t.certificationexpires as certificationexpire
from physician ph
join undergoes u on ph.employeeid = u.physician
join trained_in t
    on ph.employeeid = t.physician
where u.proceduredate > t.certificationexpires;

---5 number
select 
     p.name as patientname,
     a.starttime as appointment,
     ph.name as physicianname
from patient p
join appointment a 
    on p.ssn = a.patient
join physician ph
    on a.physician = ph.employeeid
order by a.starttime;

---6 number 


---7 number 

---8 number 
select 
     SUBSTRING(phone, 1,3) as areacode,
     count(*) as usagecount
from patient
group by substring(phone, 1, 3)
order by usagecount desc;

--- 9 number 
CREATE VIEW generalmedicinedoctors AS
SELECT
    ph.name AS physicianname,
    ph.position AS physicianposition
FROM physician ph
JOIN affiliated_with a
    ON ph.employeeid = a.physician
JOIN department d
    ON a.department = d.departmentid
WHERE d.name = 'General Medicine'
  AND a.primaryaffiliation = 1;

  select * from generalmedicinedoctors;
--- 8hourse 
select n.name as nursename,
       datediff(hour,oc.starttime,oc.endtime) as shifthours
from nurse n
join on_call oc on n.employeeid = oc.nurse 
where datediff(hour,oc.starttime,oc.endtime) >=  8;
