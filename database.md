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

### 3497. Analyze Subscription Conversion 

```sql
select t1.user_id , trial_avg_duration , paid_avg_duration from (
select user_id ,ROUND(SUM(activity_duration) * 1.0 / COUNT(activity_duration), 2) as trial_avg_duration 
 from UserActivity
where user_id in (
select distinct user_id from UserActivity where activity_type  = 'paid'
) and activity_type = 'free_trial'
group by user_id ) t1 
left join  (
select user_id ,ROUND(SUM(activity_duration) * 1.0 / COUNT(activity_duration), 2) as paid_avg_duration
 from UserActivity
where user_id in (
select distinct user_id from UserActivity where activity_type  = 'paid'
) and activity_type = 'paid'
group by user_id 
) t2 on t2.user_id = t1.user_id
```

### 1907. Count Salary Categories

```sql

select ti.category as category , 
COALESCE(tf.accounts_count, ti.val) AS accounts_count
from (
SELECT 'Low Salary' AS category, 0 AS val
UNION ALL
SELECT 'Average Salary', 0
UNION ALL
SELECT 'High Salary', 0) as ti
left join  (
select category , 
count(account_id) as accounts_count from 
(
SELECT account_id,
case 
when income < 20000 then 'Low Salary'
when income between 20000 and 50000 then 'Average Salary'
when income > 50000 then 'High Salary'
end as category
FROM Accounts
) t1
group by category
) tf on tf.category = ti.category
```

### 184. Department Highest Salary

```sql
select Department.name as Department , Employee.name as Employee , salary as Salary  from Department 
left  join Employee on Employee.departmentId = Department.id
left join (select departmentId , max(salary) as max_salary from Employee 
group by departmentId) as tt on tt.departmentId = Employee.departmentId
where salary = max_salary
```

### 602. Friend Requests II: Who Has the Most Friends

```sql
SELECT T1.I as id , COUNT(T1.I) as num FROM (SELECT requester_id AS I FROM RequestAccepted
UNION ALL 
SELECT accepter_id AS I FROM RequestAccepted) T1
GROUP BY T1.I
Having  COUNT(T1.I) = (
select max(tq.count_i) from (
SELECT T1.I , COUNT(T1.I) as COUNT_i FROM (SELECT requester_id AS I FROM RequestAccepted
UNION ALL 
SELECT accepter_id AS I FROM RequestAccepted) T1
GROUP BY T1.I) as tq
)
```

### 3220. Odd and Even Transactions

```sql
SELECT transaction_date,sum( case when amount %2 != 0 then amount else 0 end ) as odd_sum,sum( case when amount %2 = 0 then amount else 0 end ) as even_sum FROM transactions
group by transaction_date
order by transaction_date
```

### 607. Sales Person

```sql
select name from SalesPerson 
where sales_id not in (select distinct sales_id from Company
left join Orders on Orders.com_id = Company.com_id
where Company.name = 'red' and sales_id is not null)
```

### 570. Managers with at Least 5 Direct Reports

```sql
select name from Employee where id  in (
select managerId  from Employee 
group by managerId
Having count(id) >= 5
);
```

### 3808. Find Emotionally Consistent Users

```sql
select t1.user_id, reaction as dominant_reaction, round(r * 1.0 /t_r , 2) as reaction_ratio from (
select user_id , reaction , count(*) as r  from reactions
group by user_id , reaction
) t1 
left join  (
select user_id  , count(*) as t_r  from reactions
group by user_id ) t2  on 
t2.user_id = t1.user_id
where t_r >= 5 and ( r * 1.0 /t_r ) >= 0.6
order by reaction_ratio desc , user_id asc
```

### 1158. Market Analysis I

```
select user_id as buyer_id , join_date , case when orders_in_2019 is null then 0 else orders_in_2019 end as orders_in_2019  from Users 
left join (
select buyer_id , count(*) as orders_in_2019 from Orders
where year(Orders.order_date) = '2019'
group by buyer_id
) t1 on t1.buyer_id = Users.user_id
```

### 3657. Find Loyal Customers

```sql
select customer_id   from  customer_transactions
group by customer_id
having count(case when transaction_type = 'purchase' then 1 end ) >= 3 
and DATEDIFF(DAY ,MIN(transaction_date), Max(transaction_date)) >= 30 
and ((count(case when transaction_type = 'refund' then 1 end ) * 1.0) /count(transaction_type) ) < 0.2
```

### 1393. Capital Gain/Loss

```sql
select stock_name ,
sum (case when operation = 'Sell' then price end ) -
sum(case when operation = 'Buy' then price end) 
as capital_gain_loss 
from Stocks
group by stock_name
```




``sql
SELECT w1.id
FROM Weather w1
JOIN Weather w2
ON w1.recordDate = DATE_ADD(w2.recordDate, INTERVAL 1 DAY)
WHERE w1.temperature > w2.temperature;

```