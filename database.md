# Database 

### 181. Employees Earning More Than Their Managers

```sql
select Employee.name as Employee   from Employee  
left join Employee as new_emp on new_emp.id = Employee.managerId
where Employee.salary > new_emp.salary  
```

### 577. Employee Bonus
```sql 
select name , bonus from Employee
left join Bonus on Bonus.empId  = Employee.empId       
where bonus < 1000 or bonus is null
```