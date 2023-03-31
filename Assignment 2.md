## Assignment No. 2 (Insert, Select, Update, Delete, operators, functions, set

## operator, all constraints, synonym, sequence)

Account(Acc_no, branch_name,balance)
branch(branch_name,branch_city,assets)
customer(cust_name,cust_street,cust_city)
Depositor(cust_name,acc_no)
Loan(loan_no,branch_name,amount)
Borrower(cust_name,loan_no)
Solve following query:
Create above tables with appropriate constraints like primary key, foreign key, check constrains,


create table branch(
branch_name varchar2(400) primary key,
branch_city varchar2(400),
assets varchar2(400)
);

create table account(
acc_no number primary key,
branch_name varchar2(400) references branch(branch_name),
balance number
);


create table customer(
cust_name varchar2(400) primary key,
cust_street varchar2(400),
cust_city varchar(400)
);

create table depositor(
cust_name varchar2(400) references customer(cust_name),
acc_no number references account(acc_no)
);

create table loan(
loan_no number primary key,
branch_name varchar2(400) references branch(branch_name),
amount number
);

create table borrower(
cust_name varchar2(400) references customer(cust_name),
loan_no number references loan(loan_no)
);

## Q1. Find the names of all branches in loan relation.

select * from loan;

## Q2. Find all loan numbers for loans made at Akurdi Branch with loan amount > 12000.

select loan_no from loan where branch_name='Akurdi' and amount>12000;

## Q3. Find all customers who have a loan from bank. Find their names, loan_no and loan
amount.

select b.cust_name,l.loan_no,l.amount from borrower b,loan l on b.loan_no=l.loan_no;


## Q4. List all customers in alphabetical order who have loan from Akurdi branch.

select cust_name from borrower where loan_no in (select loan_no from loan where branch_name='akurdi') order by cust_name;


## Q5. Find all customers who have an account or loan or both at bank.

select * from borrower union all select * from depositor;

## Q6. Find all customers who have both account and loan at bank.

select * from borrower intersect all select * from depositor;

## Q7. Find all customer who have account but no loan at the bank.

select * from depositor minus select * from borrower

## Q8. Find average account balance at Akurdi branch.

select avg(balance) from account where branch_name='akurdi';

## Q9. Find the average account balance at each branch

select branch_name , avg(balance) from account natural join depositor
group by branch_name;

## Q10. Find no. of depositors at each branch.

select count(Distinct cust_name),branch_name
from account natural join depositor
group by branch_name;

## Q11. Find the branches where average account balance > 12000.

select branch_name from account
group by branch_name
having avg(balance)>12000

## Q12. Find number of tuples in customer relation.

select count(distinct cust_name) from customer;

## Q13. Calculate total loan amount given by bank.

select sum(amount) from loan;

## Q14. Delete all loans with loan amount between 1300 and 1500.

delete from loan where amount between 1300 and 1500;

## Q15. Delete all tuples at every branch located in Nigdi.

delete from account where branch_name in (select branch_name from branch where branch_city = 'Nigdi');

## Q.16. Create synonym for customer table as cust.

create synonym cust for customer;

## Q.17. Create sequence roll_seq and use in student table for roll_no column.

create sequence roll_seq 
start with 1
increment by 1
minvalue 1
maxvalue 1000;









