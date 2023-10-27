create database Project;
use project;
select * from finance1;
select * from finance2;
#truncate finance2;
desc finance1;
desc finance2;
select * from finance2;

## KPI-1 
# Year-wise loan amount Stats

select year(issue_d),sum(loan_amnt) from finance1
group by year(issue_d);

## KPI-2
# Grade and subgrade wise revol_bal

select finance1.grade, finance1.sub_grade,sum(finance2.revol_bal) Total 
from finance1 join finance2
on finance1.id=finance2.id
group by finance1.grade, finance1.sub_grade order by grade,sub_grade asc;

## KPI-3
#Total Payment for Verified Status Vs Total Payment for Non-Verified Status

SELECT f1.verification_status,sum(f2.total_pymnt) as total_payment
from finance1 as f1
Join finance2 as f2 on f1.id = f2.id
group by f1.verification_status
order by f1.verification_status;

##KPI-4
#State wise and last_credit_pull_d wise loan status

SELECT f1.addr_state, YEAR(f2.last_credit_pull_d) AS last_credit_pull_year,
loan_status,COUNT(*) AS total_loan_status_count
FROM finance1 AS f1
JOIN
finance2 AS f2 ON f1.id = f2.id
GROUP BY f1.addr_state, last_credit_pull_year,loan_status
ORDER BY f1.addr_state, last_credit_pull_year;


## KPI-5
#Home ownership Vs last payment date stats

SELECT f1.home_ownership, Year(f2.last_pymnt_d) AS last_payment_date_Year,
COUNT(f2.last_pymnt_d) AS total_last_payment_dates
FROM finance1 AS f1
JOIN
finance2 AS f2 ON f1.id = f2.id
GROUP BY f1.home_ownership, last_payment_date_Year
order by last_payment_date_Year;
