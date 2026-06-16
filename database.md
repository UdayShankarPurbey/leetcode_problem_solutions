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

### 586. Customer Placing the Largest Number of Orders

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

### 608. Tree Node

```sql
select id ,
case when p_id is null then  'Root'
when  id  not in (select distinct t.p_id from tree t where t.p_id is not null) then 'Leaf'
else 'Inner' end as type   
from tree
```

### 3475. DNA Pattern Recognition

```sql
select 
*,
case when SUBSTR(dna_sequence, 1, 3) = 'ATG' then 1 else 0 end as  has_start,
case when FIND_IN_SET(REVERSE(SUBSTR(REVERSE(dna_sequence), 1, 3) ), 'TAA,TAG,TGA') = 0  then 0 else 1 end as  has_stop,
case when dna_sequence like '%atat%' then 1 else 0 end as  has_atat,
case when dna_sequence like '%ggg%' then 1 else 0 end as  has_ggg
from samples
order by sample_id asc;
```

### 596. Classes With at Least 5 Students

```sql
select class from Courses
group by class
having count(*) >= 5
```

### 1050. Actors and Directors Who Cooperated At Least Three Times

```sql 
# Write your MySQL query statement below
select actor_id , director_id from ActorDirector
group by director_id , actor_id
having count(actor_id) >= 3
```

### 1587. Bank Account Summary II

```sql
SELECT u.name, SUM(amount) as balance
FROM Transactions t
LEFT JOIN Users u ON u.account=t.account GROUP BY t.account
HAVING SUM(amount)>10000
```

### 1141. User Activity for the Past 30 Days I

```sql
select activity_date as day , count(distinct user_id) as active_users from Activity
WHERE activity_date BETWEEN '2019-06-28' AND '2019-07-27'
group by activity_date 
```