# Finance Analysis

link to the case study - https://www.steeldata.org.uk/SQL4.html

## 1. What are the names of all the customers who live in New York?
```
select Concat(FirstName,' ' ,LastName) as full_name
from Customers
where city = 'New York'
```
## 2. What is the total number of accounts in the Accounts table?
```
select count(AccountID)
from Accounts
```
## 3. What is the total balance of all checking accounts?
```
select sum(Balance) as Total_checking_Balance
from Accounts
where AccountType = 'Checking'
```
## 4. What is the total balance of all accounts associated with customers who live in Los Angeles?
```
select sum(balance) as total_bal_Los_anegeles
from Accounts a
join Customers c
on a.CustomerID= c.CustomerID
where city = 'Los Angeles'
```
## 5. Which branch has the highest average account balance?
```
select top 1 AVG(a.Balance) as a_bal, b.BranchID, b.BranchName, b.City
from Accounts a
join Branches b
on b.BranchID = a.BranchID
group by b.BranchID, b.BranchName, b.City
order by 1 desc
```

## 6. Which customer has the highest current balance in their accounts?
```
select top 1 c.CustomerID, concat(c.FirstName,' ',c.LastName) as full_name, sum(a.balance)
from Customers c
join Accounts a
on a.CustomerID = c.CustomerID
group by  c.CustomerID, concat(c.FirstName,' ',c.LastName)
order by 3 desc
```
## 7. Which customer has made the most transactions in the Transactions table?
```
select top 2 count(t.AccountID) as transaction_num, a.CustomerID, concat(c.FirstName,' ',c.LastName) as full_name
from Transactions t
join Accounts a
on a.AccountID = t.AccountID
join Customers c
on c.CustomerID = a.CustomerID
group by a.CustomerID, concat(c.FirstName,' ',c.LastName)
order by 1 desc
```
## 8. Which branch has the highest total balance across all of its accounts?
```
select sum(Balance) as total_balance,Accounts.BranchID, Branches.BranchName
from Accounts
JOIN Branches 
ON Branches.BranchID = Accounts.BranchID
group by Accounts.BranchID,Branches.BranchName
ORDER BY 1 DESC
```

## 9. Which customer has the highest total balance across all of their accounts, including savings and checking accounts?
```
select top 1 sum(Balance) as total_balance,c.CustomerID, concat(c.FirstName,' ',c.LastName) as full_name
from Accounts
JOIN Customers c
ON c.CustomerID = Accounts.CustomerID
where AccountType <> 'Credit Card'
group by c.CustomerID, concat(c.FirstName,' ',c.LastName)
ORDER BY 1 DESC
```

## 10. Which branch has the highest number of transactions in the Transactions table?
```
select Top 2 count(t.TransactionID) , b.BranchID, b.BranchName, City
FROM Transactions t
join Accounts a
on a.AccountID = t.AccountID
join Branches b
on b.BranchID = a.BranchID
group by b.BranchID,b.BranchName,City
```
