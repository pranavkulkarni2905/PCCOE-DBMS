## 1. Create following Tables
## cust_mstr(cust_no,fname,lname)
## add_dets(code_no,add1,add2,state,city,pincode)

## Retrieve the address of customer Fname as 'xyz' and Lname as 'pqr'

create table customer(
cust_no number primary key,
fname varchar2(400),
lname varchar2(400)
);

create table address(
cust_no number references customer(cust_no),
add1 varchar2(400),
add2 varchar2(400),
state varchar2(400),
city varchar2(400),
pincode varchar2(400)
);

insert into customer values(101,'xyz','pqr');
insert into customer values(102,'abc','lmn');


insert into address values(101,'pune','akurdi','MH','pune','411011');
insert into address values(102,'mumbai','pimpri','Pune','123432');

## select * from address where cust_no in (select cust_no from address where fname='xyz' and lname='pqr');


2.Create following Tables
cust_mstr(custno,fname,lname)
acc_fd_cust_dets(codeno,acc_fd_no)
fd_dets(fd_sr_no,amt)

## List the customer holding fixed deposit of amount more than 5000 

create table customer(
custno number primary key,
fname varchar2(400),
lname varchar2(400)
);

create table account_fd(
codeno number references customer(custno),
acc_fd_no varchar2(100) primary key
);

create table fd_details(
fd_sr_no varchar2(100) references account_fd(codeno),
amt number
);


insert into customer values(101,'pranav','kulkarni');
insert into customer values(102,'ritish','shelke');

insert into account_fd values(101,'f11');
insert into account_fd values(102,'f12');

insert into fd_details values('f11',14000);
insert into fd_details values('f12',2000);

## select * from customer where custno in (select codeno from account_fd where acc_fd_no in (select fd_sr_no from fd_details where amt>5000));

3. Create following Tables
emp_mstr(e_mpno,f_name,l_name,m_name,dept,desg,branch_no)
branch_mstr(name,b_no)

## List the employee details along with branch names to which they belong

create table branch(
name varchar2(400),
branch_no varchar2(400) primary key
);

create table emp(
emp_no number primary key,
fname varchar2(400),
lname varchar2(400),
mname varchar2(400),
dept varchar2(400),
desg varchar2(400),
branch_no varchar2(400) references branch(branch_no)
);

insert into branch values('AMAZON Akurdi','b101');
insert into branch values('AMAZON Pimpri','b102');

insert into emp values(101,'pranav','kulkarni','digambar','project','SDE1','b101');
insert into emp values(102,'gauri','ghodake','kishor','HR','Manager','b102');

## select emp.emp_no , emp.fname,emp.lname,emp.mname,emp.dept,emp.desg,emp.branch_no,branch.name from emp inner join branch on emp.branch_no=branch.branch_no;


4. Create following Tables
emp_mstr(emp_no,f_name,l_name,m_name,dept)
cntc_dets(code_no,cntc_type,cntc_data)

## List the employee details along with contact details using left outer join & right join



create table emp(
emp_no number primary key,
fname varchar2(400),
lname varchar2(400),
mname varchar2(400),
dept varchar2(400),
);

create table contact_details(
code_no number,
contact_type varchar2(400),
contact_data varchar2(400)
);

insert into emp values (101,'pranav','kulkarni','digambar','computer');
insert into emp values (102,'gauri','ghodake','kishor','IT');
insert into emp values (103,'ritsih','sheleke','Vijay','Mechanical');

insert into contact_details values(101,'phone','9879878');
insert into contact_details values(102,'email','abc@gmail.com');
insert into contact_details values(104,'linedin','linkedin/pranavk');

## select emp.emp_no,emp.fname,emp.lname,emp.mname,emp.dept,contact_details.contact_type,contact_details.contact_data from emp left join contact_details on emp.emp_no=contact_details.code_no;

## select emp.emp_no,emp.fname,emp.lname,emp.mname,emp.dept,contact_details.contact_type,contact_details.contact_data from emp right join contact_details on emp.emp_no=contact_details.code_no;



