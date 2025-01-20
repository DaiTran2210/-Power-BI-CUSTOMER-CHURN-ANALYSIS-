# [Power BI] CUSTOMER CHURN ANALYSIS
## I. Introduction
### 1. Introduction to Dataset
- User churn happens when customers stop using a product or service over time, which can have a negative impact on the business.
- Figuring out why users churn is super important because it helps companies come up with better ways to keep their customers happy and improve what they offer.
- This dataset includes a dim table with details about users of a telecommunications network company, like demographic information and insights about user churn.
### 2. Data Dictionary
![image](https://github.com/user-attachments/assets/ada181f3-5c56-4494-8769-d68733b24628)
### 3. Business Questions
- Build a dashboard for managers that gives a clear overview of user churn status and highlights which users are part of the churn group.
- Come up with creative solutions to tackle the issue and help reduce user churn.
## II. Design Thinking Method
I applied 5 steps of Design Thinking to this project
### Step 1: Emphthize
![step1](https://github.com/user-attachments/assets/033e4482-925b-4bbf-94f1-532718a4a68d)
### Step 2 - Define
![step2](https://github.com/user-attachments/assets/afa15934-13a7-4ca4-9e58-28cf7e794c1d)

### Step 3 - Ideate
![step3](https://github.com/user-attachments/assets/7a52d34c-bad9-4e35-80e2-d016d135c48e)

### Step 4 - Prototype
![step4](https://github.com/user-attachments/assets/0db33c39-9045-4ccb-80cf-f53d028ef586)

### Step 5 - Review
![step5](https://github.com/user-attachments/assets/464325fb-4d37-4e51-82b2-a125b871f414)
## III. Visualization
### 1. Customer Overview
![image](https://github.com/user-attachments/assets/d140af81-6aa0-42e6-900a-d9ca8d7ed137)
### 2. Customer Detail
![image](https://github.com/user-attachments/assets/fa0ca600-49a1-417c-aece-b2011e6b8707)
### 3. Churn Reason
![image](https://github.com/user-attachments/assets/4fa4725c-ec65-4e5b-bf6e-78cc58ec1834)
## IV. Calculated columns & Measures
### Calculated columns
#### Total Call
````
Total Call = Users[Customer Service Calls] + Users[Intl Calls] + Users[Local Calls]
````
### Measures
#### Total users with Device Protection & Online Backup
````
%dpob_all = calculate(count(Users[Device Protection & Online Backup]), filter(users, Users[Device Protection & Online Backup] = "Yes" )) / [total_count]
````
#### Churned users with Device Protection & Online Backup 
````
%dpob_churn = calculate(count(Users[Device Protection & Online Backup]), filter(users, and(Users[Device Protection & Online Backup] = "Yes",  Users[Churn Label] = "Yes"))) / [churned_count]
````
#### Total users with groups
````
%group_all = calculate(count(Users[Group]), filter(users, Users[Group] = "Yes")) / [total_count]
````
#### Churned users with groups
````
%group_churn = calculate(count(Users[Group]), filter(users, and(Users[Group] = "Yes", Users[Churn Label] = "Yes"))) / [churned_count]
````
#### Total international active calls
````
%intl_active_all = calculate(count(Users[Intl Active]), filter(users,Users[Intl Active] = "Yes")) / [total_count]
````
#### Churned international active calls
````
%intl_active_churn = calculate(count(Users[Intl Active]), FILTER(users,and(Users[Intl Active] = "Yes" , Users[Churn Label] = "Yes"))) / [churned_count]
````
#### Users that over 30 years old
````
%Over30All = calculate(count(Users[Age_condition]), filter(Users,Users[Age_condition] = ">=30")) / [total_count]
````

#### Churned users that over 30 years old
````
%Over30churn = calculate(count(Users[Age_condition]), filter(Users,and(Users[Age_condition] = ">=30",Users[Churn Label] = "Yes"))) / [churned_count]
````

#### Total users with Unlimited Data Plan
````
%udp_all = calculate(count(Users[Unlimited Data Plan]), filter(users, Users[Unlimited Data Plan] = "Yes")) / [total_count]
````

#### Churned users with Unlimited Data Plan
````
%udp_churn = calculate(count(Users[Unlimited Data Plan]), filter(users, and(Users[Unlimited Data Plan] = "Yes" , Users[Churn Label] = "Yes"))) / [churned_count]
````

#### Total users under 30 years old
````
%Under30All = calculate(count(Users[Age_condition]), filter(Users,Users[Age_condition] = "<30")) / [total_count]
````

#### Churned users under 30 years old
````
%Under30churn = calculate(count(Users[Age_condition]), filter(Users,and(Users[Age_condition] = "<30",Users[Churn Label] = "Yes"))) /[churned_count]
````

#### Average Users with Monthly Charge
````
avg_monthly_charge_all = calculate(average(Users[Monthly Charge]))
````

#### Churned Users with Monthly Charge
````
avg_monthly_charge_churn = calculate(sum(Users[Monthly Charge]),filter(users,Users[Churn Label] = "Yes")) / [churned_count]
````

#### Average Users with Total Charges
````
avg_total_charge_all = calculate(average(Users[Total Charges]))
````

#### Churned Users with Total Charges
````
avg_total_charge_churn = calculate(SUM(Users[Total Charges]),Users[Churn Label] = "Yes") / [churned_count]
````

#### Total Churned Users
````
churned_count = calculate(count(Users[Churn Label]),filter(users,Users[Churn Label] = "Yes"))
````

#### Percent Churned
````
Percent_Churn = [churned_count] / [total_count]
````

#### Total Users
````
total_count = countrows(users)
````

## V. Insights
- Competitors are offering better deals and prices compared to our company.  
- Our customer service needs improvement—customers who churn tend to call customer service more often, with an average of 2.4 calls compared to the norm.  
- Customers using 0–10 GB of monthly data but subscribing to the Unlimited Data plan are more likely to churn than others.  
- Customers on "month-to-month" contracts have a significantly high churn rate of nearly 90%.
## VI. Recommendations

- Focus on improving customer service by streamlining the problem-solving process—help customers quickly and avoid situations where they have to call multiple times to get an issue resolved.
- Provide both online and phone support to address customer concerns more effectively.
- Offer special incentives for customers on month-to-month contracts, like top-up bonuses or discounted data packages, to keep them engaged.
- Rework the Unlimited Data plan to either lower the price or create a better value data package tailored for customers using 0–10 GB monthly.
- Introduce exciting offers for new customers, but don’t forget to reward loyal customers with meaningful incentives. Since 45% of churn happens because competitors have better deals, we need to stand out with both competitive pricing and great customer appreciation programs.
