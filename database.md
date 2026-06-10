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

### 595. Big Countries

```sql 
select name        , population , area from World
where area >= 3000000 or population >= 25000000
```

### 1193. Monthly Transactions I

```sql
# Write your MySQL query statement below

SELECT DATE_FORMAT(trans_date , '%Y-%m') as month , country , count(*) as trans_count,  
SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END) AS approved_count,sum(amount) as trans_total_amount ,
    SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END) AS approved_total_amount
  FROM Transactions
group by DATE_FORMAT(trans_date , '%Y-%m') , country 
order by DATE_FORMAT(trans_date , '%Y-%m') , country , trans_count
```

### 196. Delete Duplicate Emails

```sql
DELETE
FROM
person
WHERE Id NOT IN
(
SELECT minid
FROM
(SELECT email, min(id) as minid
FROM Person
GROUP BY email ) test)
```

### 183. Customers Who Never Order

```sql
select name as Customers   from Customers 
left join Orders on Orders.customerId  = Customers.id
where Orders.id is null  
```

### 584. Find Customer Referee

```sql
select name  from Customer where referee_id  not in (2) or referee_id is null
```

### 511. Game Play Analysis I

```sql
select player_id ,min(event_date) as first_login     from Activity
group by player_id 
```

### 586.p

```sql
select customer_number  from Orders
group by customer_number
    order by count(*) desc
    limit 1
    ```

### Q3. Not Boring Movies

```sql
select * from Cinema where (id %2 != 0) 
and description != "boring"
order by rating desc
```

### 619. Biggest Single Number

```sql
select max(num) as num from (
    select num from MyNumbers
group by num 
having count(num) = 1
) a
```