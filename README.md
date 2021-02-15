# Classification- Default Payments of Credit Card Clients in Taiwan from 2005

## Objective
Credit card is a commonly used transaction method in modern society and one of the main business of banks. For banks, it helps the bank to generate interest revenue but at the same time, it raise the liquidity risk and credit risk to the bank. In order to control the cash flow and risk, detecting the customers with default payment next month could play an important roles of estimating the potential **cash flow and risk management**.

**For quick summary**, please refer to our [Powerpoint](https://drive.google.com/file/d/1GUbzx7Nd61jiQ8lFu37YPtEOmOMXg0r4/view?usp=sharing).

## Dataset
This dataset contains information on default payments, demographic factors, credit data, history of payment, and bill statements of credit card clients in Taiwan from April 2005 to September 2005.

The target variable is the default.payment.next.month(1=yes, 0=no) which is if the the customer would have **Default Payment Next Month** (October 2005).
There are 24 features which include the payment status, payment amount and bill amount each month from April 2005 to September 2005.

The dataset can be found on [Kaggle](https://www.kaggle.com/uciml/default-of-credit-card-clients-dataset) or at [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/default+of+credit+card+clients)  

This dataset has inaccurate labels for the payment status and default payment next month(target variable). The authors of this dataset did not explain the rules or how to read the dataset clearly. We find the **rules of payment status** below for etter understanding: 
(Or you can find the rules in the notebook with the tables as clues)  

### Rules of Payment Status:  
#### General Rule :
The bill amount of time T should be repaid next month ( payment amount of time T+1) where the payment status of this bill is indicated as payment status at time T e.g. bill amount of April should be matched with the payment amount of May in order to settle the bill which will give a payment status of -1 (paid in full) in April. In other words, we should look at bill of the first month and payment_amount of the second month and payment_status of the first month.  

- payment_status_sept is redundant as we have no information about the payment amount in October
- payment_amount_apr is also redundant as it is refering to the bill of March which we have no information about it  

#### Rule 1:
If the customer has payment of 0 continously, the payment status will add 1 accordingly(i.e. third month of no payment will be 3, the forth month of continuous 0 payment will be 4, so on...)

#### Rule 2:
If the customer has payment of less than a particular percentage of the bill ( varies amongst customers which we do not know)

- If the payment is less 5% of the bill amount for some customers with the payment status 0 in previous month, it counts as late payment of 2 months
- If the payment is less 5% of the bill amount for some customers with the payment status <0 in previous month, the payment status will increase 1 ( e.g. 3->4)
#### Rule 3:
If the customer has payment more than a particular percentage of the bill but not in full, it counts as the use of revolving credit(class 0)

### Incorrect Labels for Target:
There are **317 customers** have **no consumption** at all but some of them have **payment status 1** (1 month late payment) in September and **default payment next month** which do **NOT make sense**. Therefore we suggest an assignment of 0 (no default payment) for those customers in the feature engineering part.

## Key Findings:
1. Low Repayment Revenue
   - The majority of the customer pay less than 200,000 NTD every month regardless their bill amount. There are two groups/trends of the customers' payment and bill amount. The first group is they pay what they owe or proportionally (the inclined line). The second group is they barely pay or even 0 payment no matter how big the bill amount is. At least 8000 customers pay less than 1,000 NTD or **even 0 NTD** each month which align with the finding above. This is a **warning sign** that the **credit risk** is increasing as customers cannot pay their debts.
   
2. Low Usage Rate of the Credit Cards
   - The distribution of the bill amount every month is right-skewed. Around 6000 to 8000 customers have their bill amount less than 5000 NTD every month which shows that the credit card of our bank may not be the first choice of their payment method.

3. Late Payment Issue
   - There are a group of customers keep delaying their payment while keep spending with the credit cards. People who have the payment delay for two months have a high ratio of default next month (October). In September, a quarter of customers who repay one month later have default payment next month in October. This situation does not exist in other months as almost no one repay one month later.
   
## Suggestions :
1. Customer Retention Program
   - More than 860 customers have not used the credit cards for the past 6 months, the marketing team could organize campaigns or promotions to encourage the utilization of the cards and increase the interest revenue of the bank.
   
2. Take Action on Delinquent Accounts
   - At least 3000 customers have late payment more than 2 months. The longer the repayment, the more difficult the debt collection. The bank should remind the customers to pay every month or at least repay the minimum amount, or further actions should be taken if the debt is not collectable after 4 months.  
   

## Acknowledgements
Lichman, M. (2013). UCI Machine Learning Repository [http://archive.ics.uci.edu/ml]. Irvine, CA: University of California, School of Information and Computer Science.
