# DannyMaSQLChallengeWeek3
I started the DannyMa 8 week SQL challenge to practice my SQL skills. The week 3 is about foodie_fi. A <code class="language-plaintext highlighter-rouge">subscription-based</code> company. This repository contains the solutions for each question asked. I did this using <code class="language-plaintext highlighter-rouge">PostgreSQL</code>
## INTRODUCTION
Subscription based businesses are super popular and Danny realised that there was a large gap in the market - he wanted to create a new streaming service that only had food related content - something like Netflix but with only cooking shows!
Danny finds a few smart friends to launch his new startup Foodie-Fi in 2020 and started selling monthly and annual subscriptions, giving their customers unlimited on-demand access to exclusive food videos from around the world!
Danny created Foodie-Fi with a data driven mindset and wanted to ensure all future investment decisions and new features were decided using data. This case study focuses on using subscription style digital data to answer important business questions.

![case-study-3-erd](https://github.com/Mave-t-ech/DannyMaSQLChallengeWeek3/assets/111718556/1d8a0b6f-313a-4f7c-b4c4-55414e0b66e9)

## Table 1: Plans 
Customers can choose which plans to join Foodie-Fi when they first sign up.
Basic plan customers have limited access and can only stream their videos and is only available monthly at $9.90
Pro plan customers have no watch time limits and are able to download videos for offline viewing. Pro plans start at $19.90 a month or $199 for an annual subscription.
Customers can sign up to an initial 7 day free trial will automatically continue with the pro monthly subscription plan unless they cancel, downgrade to basic or upgrade to an annual pro plan at any point during the trial.
When customers cancel their Foodie-Fi service - they will have a churn plan record with a null price but their plan will continue until the end of the billing period.

<div class="responsive-table">

  <table>
    <thead>
      <tr>
        <th>plan_id</th>
        <th>plan_name</th>
        <th>price</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>0</td>
        <td>trial</td>
        <td>0</td>
      </tr>
      <tr>
        <td>1</td>
        <td>basic monthly</td>
        <td>9.90</td>
      </tr>
      <tr>
        <td>2</td>
        <td>pro monthly</td>
        <td>19.90</td>
      </tr>
      <tr>
        <td>3</td>
        <td>pro annual</td>
        <td>199</td>
      </tr>
      <tr>
        <td>4</td>
        <td>churn</td>
        <td>null</td>
      </tr>
    </tbody>
  </table>

</div>

<h3 id="table-2-subscriptions">Table 2: subscriptions</h3>

<p>Customer subscriptions show the exact date where their specific <code class="language-plaintext highlighter-rouge">plan_id</code> starts.</p>
<p>If customers downgrade from a pro plan or cancel their subscription - the higher plan will remain in place until the period is over - the <code class="language-plaintext highlighter-rouge">start_date</code> in the <code class="language-plaintext highlighter-rouge">subscriptions</code> table will reflect the date that the actual plan  changes.</p>
<p>When customers upgrade their account from a basic plan to a pro or annual pro plan - the higher plan will take effect straightaway.</p>
<p>When customers churn - they will keep their access until the end of their current billing period but the <code class="language-plaintext highlighter-rouge">start_date</code> will be technically the day they decided to cancel their service.</p>

<div class="responsive-table">

  <table>
    <thead>
      <tr>
        <th>customer_id</th>
        <th>plan_id</th>
        <th>start_date</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>1</td>
        <td>0</td>
        <td>2020-08-01</td>
      </tr>
      <tr>
        <td>1</td>
        <td>1</td>
        <td>2020-08-08</td>
      </tr>
      <tr>
        <td>2</td>
        <td>0</td>
        <td>2020-09-20</td>
      </tr>
      <tr>
        <td>2</td>
        <td>3</td>
        <td>2020-09-27</td>
      </tr>
      <tr>
        <td>11</td>
        <td>0</td>
        <td>2020-11-19</td>
      </tr>
      <tr>
        <td>11</td>
        <td>4</td>
        <td>2020-11-26</td>
      </tr>
      <tr>
        <td>13</td>
        <td>0</td>
        <td>2020-12-15</td>
      </tr>
      <tr>
        <td>13</td>
        <td>1</td>
        <td>2020-12-22</td>
      </tr>
      <tr>
        <td>13</td>
        <td>2</td>
        <td>2021-03-29</td>
      </tr>
      <tr>
        <td>15</td>
        <td>0</td>
        <td>2020-03-17</td>
      </tr>
      <tr>
        <td>15</td>
        <td>2</td>
        <td>2020-03-24</td>
      </tr>
      <tr>
        <td>15</td>
        <td>4</td>
        <td>2020-04-29</td>
      </tr>
      <tr>
        <td>16</td>
        <td>0</td>
        <td>2020-05-31</td>
      </tr>
      <tr>
        <td>16</td>
        <td>1</td>
        <td>2020-06-07</td>
      </tr>
      <tr>
        <td>16</td>
        <td>3</td>
        <td>2020-10-21</td>
      </tr>
      <tr>
        <td>18</td>
        <td>0</td>
        <td>2020-07-06</td>
      </tr>
      <tr>
        <td>18</td>
        <td>2</td>
        <td>2020-07-13</td>
      </tr>
      <tr>
        <td>19</td>
        <td>0</td>
        <td>2020-06-22</td>
      </tr>
      <tr>
        <td>19</td>
        <td>2</td>
        <td>2020-06-29</td>
      </tr>
      <tr>
        <td>19</td>
        <td>3</td>
        <td>2020-08-29</td>
      </tr>
    </tbody>
  </table>

</div>

<h3 id="a-customer-journey">A. Customer Journey</h3>

<p>Based off the 8 sample customers provided in the sample from the <code class="language-plaintext highlighter-rouge">subscriptions</code> table, write a brief description about each customer’s onboarding journey.</p>

<p>Try to keep it as short as possible - you may also want to run some sort of join to make your explanations a bit easier!</p>

<h3 id="b-data-analysis-questions">B. Data Analysis Questions</h3>

<ol>
  <li>How many customers has Foodie-Fi ever had?</li>
  <li>What is the monthly distribution of <code class="language-plaintext highlighter-rouge">trial</code> plan <code class="language-plaintext highlighter-rouge">start_date</code> values for our dataset - use the start of the month as the group by value</li>
  <li>What plan <code class="language-plaintext highlighter-rouge">start_date</code> values occur after the year 2020 for our dataset? Show the breakdown by count of events for each <code class="language-plaintext highlighter-rouge">plan_name</code></li>
  <li>What is the customer count and percentage of customers who have churned rounded to 1 decimal place?</li>
  <li>How many customers have churned straight after their initial free trial - what percentage is this rounded to the nearest whole number?</li>
  <li>What is the number and percentage of customer plans after their initial free trial?</li>
  <li>What is the customer count and percentage breakdown of all 5 <code class="language-plaintext highlighter-rouge">plan_name</code> values at <code class="language-plaintext highlighter-rouge">2020-12-31</code>?</li>
  <li>How many customers have upgraded to an annual plan in 2020?</li>
  <li>How many days on average does it take for a customer to an annual plan from the day they join Foodie-Fi?</li>
  <li>Can you further breakdown this average value into 30 day periods (i.e. 0-30 days, 31-60 days etc)</li>
  <li>How many customers downgraded from a pro monthly to a basic monthly plan in 2020?</li>
</ol>

<h3 id="SOLUTIONS">SOLUTIONS</h3>


<h4 id="A. Customer Journey">A. Customer Journey</h4>

Based off the 8 sample customers provided in the sample from the subscriptions table,
write a brief description about each customer’s onboarding journey.
Try to keep it as short as possible - you may also want to run some sort of join to-
make your explanations a bit easier!*/
```
SELECT customer_id, plan_name, p.plan_id, start_date
FROM foodie_fi.plans as p 
INNER JOIN foodie_fi.subscriptions as s 
ON p.plan_id = s.plan_id
WHERE customer_id <= 8;
```
#### SECTION B 
##### Question 1 How many customers has Foodie-Fi ever had?
```
SELECT COUNT (DISTINCT customer_id) total_customers
FROM foodie_fi.plans as p 
INNER JOIN foodie_fi.subscriptions as s 
ON p.plan_id = s.plan_id;
```
##### Question 2 What is the monthly distribution of trial plan start_date values for our dataset - use the start of the month as the group by value*/
```
SELECT COUNT (plan_name), Extract (month from start_date) as start_month, To_char (start_date, 'Month') as month
FROM foodie_fi.plans as p 
INNER JOIN foodie_fi.subscriptions as s 
ON p.plan_id = s.plan_id
where plan_name = 'trial'
GROUP BY To_char (start_date, 'Month'), Extract (month from start_date)
ORDER BY COUNT (plan_name);
```
```
SELECT DATE_TRUNC ('month', start_date) as start_month, COUNT(customer_id) as distribution
FROM foodie_fi.subscriptions
where plan_id = 0
GROUP BY DATE_TRUNC ('month', start_date);
```
##### Question 3 What plan start_date values occur after the year 2020 for our dataset? Show the breakdown by count of events for each plan_name*/
```
SELECT DATE_PART ('year', start_date) as year, COUNT (*) as count_of_events, plan_name
FROM foodie_fi.subscriptions as s
INNER JOIN foodie_fi.plans as p
ON p.plan_id=s.plan_id
WHERE  DATE_PART ('year', start_date) > 2020
GROUP BY DATE_PART ('year', start_date), plan_name;
```
##### <code class="language-plaintext highlighter-rouge">METHOD 2</code>
```
SELECT EXTRACT (year from start_date) as year, COUNT (*) as count_of_events, plan_name
FROM foodie_fi.subscriptions as s
INNER JOIN foodie_fi.plans as p
ON p.plan_id=s.plan_id
WHERE  EXTRACT (year from start_date) > 2020
GROUP BY EXTRACT (year from start_date), plan_name;
```
##### Question 4 What is the customer count and percentage of customers who have churned rounded to 1 decimal place?*/
```
WITH CTE AS (SELECT (SELECT COUNT (DISTINCT customer_id)
FROM foodie_fi.subscriptions) as customer_count, COUNT (DISTINCT customer_id) as churned
FROM foodie_fi.subscriptions
WHERE plan_id = 4)

SELECT CONCAT (ROUND((churned:: numeric/customer_count:: numeric):: numeric * 100,1), '%')  as percentage_churned 
FROM CTE;
```
##### Question 5 How many customers have churned straight after their initial free trial - what percentage is this rounded to the nearest whole number?
```
WITH CTE AS (
	SELECT customer_id, plan_name,
ROW_NUMBER() OVER(PARTITION BY customer_id ORDER BY start_date ASC) as row
FROM foodie_fi.subscriptions as s
INNER JOIN foodie_fi.plans as p
ON p.plan_id = s.plan_id
)

SELECT COUNT (DISTINCT customer_id) AS churned_after_trial,CONCAT (ROUND (COUNT (DISTINCT customer_id):: numeric/
		(SELECT COUNT(DISTINCT customer_id) FROM foodie_fi.subscriptions)::numeric *100,1),'%') as percentage_churn_after_trial
FROM cte
WHERE row = 2
AND plan_name = 'churn';
```
##### Question 6 What is the number and percentage of customer plans after their initial free trial?
```
WITH CTE AS (
	SELECT customer_id, plan_name,
ROW_NUMBER() OVER(PARTITION BY customer_id ORDER BY start_date ASC) as row
FROM foodie_fi.subscriptions as s
INNER JOIN foodie_fi.plans as p
ON p.plan_id = s.plan_id
)

SELECT plan_name, COUNT (customer_id) as count, 
CONCAT (ROUND(COUNT (customer_id)::numeric/(SELECT COUNT(DISTINCT customer_id) FROM foodie_fi.subscriptions)::numeric *100),'%') as percentage
FROM cte
WHERE row = 2
GROUP BY plan_name;
```
##### Question 7 What is the customer count and percentage breakdown of all 5 plan_name values at 2020-12-31?
```
WITH CTE AS (
	SELECT *,
ROW_NUMBER() OVER(PARTITION BY customer_id ORDER BY start_date DESC) as row
FROM foodie_fi.subscriptions 
	WHERE start_date <= '2020-12-31'
)

SELECT  plan_name, COUNT (customer_id), 
CONCAT(ROUND (COUNT(customer_id)::numeric/(SELECT COUNT(DISTINCT customer_id) FROM cte)::numeric *100, 1), '%') as customer_percentage
FROM CTE as c
INNER JOIN foodie_fi.plans as p
ON p.plan_id = c.plan_id
WHERE row = 1
GROUP BY plan_name;
```
##### Question 8 How many customers have upgraded to an annual plan in 2020?
```
WITH BP_Month AS (
SELECT customer_id, start_date
FROM foodie_fi.subscriptions
WHERE start_date <= '2020-12-31'
AND plan_id IN (1,2)
	)
, ANNUAL AS (
SELECT customer_id, start_date
FROM foodie_fi.subscriptions
WHERE start_date <= '2020-12-31'
AND plan_id = 3
	)
SELECT COUNT (DISTINCT A.customer_id) as upgrade
FROM BP_Month as M
INNER JOIN ANNUAL as A
ON M.customer_id = A.customer_id AND 
M.start_date < A.start_date;
```
##### Question 9 How many days on average does it take for a customer to an annual plan from the day they join Foodie-Fi?
```
WITH TRIAL AS (
	SELECT customer_id, start_date as trial_date
	FROM foodie_fi.subscriptions 
	WHERE plan_id = 0
)
, ANNUAL AS (
SELECT customer_id, start_date as annual_date
FROM foodie_fi.subscriptions
WHERE plan_id = 3
)
SELECT ROUND(AVG(annual_date - trial_date),1 ) as day_diff
FROM TRIAL as t
INNER JOIN ANNUAL as a
ON t.customer_id = a.customer_id;
```
##### Question 10 Can you further breakdown this average value into 30 day periods (i.e. 0-30 days, 31-60 days etc)
```
WITH TRIAL AS (
	SELECT customer_id, start_date as trial_date
	FROM foodie_fi.subscriptions 
	WHERE plan_id = 0
)
, ANNUAL AS (
SELECT customer_id, start_date as annual_date
FROM foodie_fi.subscriptions
WHERE plan_id = 3
)
SELECT COUNT(a.customer_id) as count_of_customers,
CASE
WHEN annual_date - trial_date <= 30 THEN '0-30 days'
WHEN (annual_date - trial_date) <= 31 THEN '31-60 days'
WHEN (annual_date - trial_date) <= 61 THEN '61-90 days'
WHEN (annual_date - trial_date) <= 91 THEN '91-120 days'
WHEN (annual_date - trial_date) <= 121 THEN '121-150 days'
WHEN (annual_date - trial_date) <= 151 THEN '151-180 days'
WHEN (annual_date - trial_date) <= 181 THEN '181-210 days'
WHEN (annual_date - trial_date) <= 211 THEN '211-240 days'
WHEN (annual_date - trial_date) <= 241 THEN '241-270 days'
WHEN (annual_date - trial_date) <= 271 THEN '271-300 days'
WHEN (annual_date - trial_date) <= 301 THEN '301-330 days'
WHEN (annual_date - trial_date) <= 331 THEN '331-360 days'
WHEN (annual_date - trial_date) <= 361 THEN '361-390 days'
END brkdwn
FROM TRIAL as t
INNER JOIN ANNUAL as a
ON t.customer_id = a.customer_id
GROUP BY 2
ORDER BY 2;
```
##### Question 11 How many customers downgraded from a pro monthly to a basic monthly plan in 2020?
```
WITH Pro_Month AS (
SELECT customer_id, start_date
FROM foodie_fi.subscriptions
WHERE start_date <= '2020-12-31'
AND plan_id = 2
	)
, BASIC AS (
SELECT customer_id, start_date
FROM foodie_fi.subscriptions
WHERE start_date <= '2020-12-31'
AND plan_id = 1
	)
SELECT COUNT (DISTINCT P.customer_id) as downgrade
FROM Pro_Month as P
INNER JOIN BASIC as B
ON P.customer_id = B.customer_id AND 
P.start_date < B.start_date;select *
from foodie_fi.subscriptions;
```
