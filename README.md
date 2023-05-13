# Prosper Loan Exploratory Data Analysis

## Introduction

This project is part of Udacity's Nanodegree Program for Data Analysts. I conducted exploratory data analysis (EDA) on Prosper's data set. Prosper is the first market lending platform in the United States, with financing loans exceeding 9 billion US dollars. The data set contains 113,937 loans. Each loan has 81 variables, including loan amount, borrower's interest rate (or interest rate), current loan status, borrower's income, borrower's employment status, borrower's credit history, and the latest payment information.

## Explore Your Data

## Data Assessing and Cleaning

### What is the structure of your dataset?

The dataset has 113,937 loans with 81 variables on each loan. I will be interested in a subset of those variables. The dataset contains 84853 loans with 28 features including  ListingCreationDate, LoanOriginalAmount, LoanStatus, ListingCategory (numeric), BorrowerState, BorrowerAPR, BorrowerRate,StatedMonthlyIncome, ProsperRating (Alpha), ProsperScore, LoanMonthsSinceOrigination, Occupation, Term, EmploymentStatus , TotalInquiries, DebtToIncomeRatio, MonthlyLoanPayment , TotalTrades, Investors, IsBorrowerHomeowner, CreditScoreRangeLower, AvailableBankcardCredit, IncomeRange and others. Variables are loan information and borrower information.


### What is/are the main feature(s) of interest in your dataset?

I'm most interested in figuring out what features are best for predicting borrower's Annual Percentage Rate (Borrower APR) for the loan and affecting the loan status and how employment status and debtToIncome ratio associates with various metrics in the dataset.

### What features in the dataset do you think will help support your investigation into your feature(s) of interest?

To study the borrower interest rate and loan status, I included  ListingCreationDate and some borrower information such as Occupation, Term, EmploymentStatus,  AvailableBankcardCredit, CreditGrade, StatedMonthlyIncome and  DebtToIncomeRatio.

1.choose subset of features important

2.drop duplicated rows based on listing number

3.convert datatypes of TotalTrades and TotalInquiries to int , ListingCreationDate to datetime

4.removed rows without ProsperRating

5.fill in missing values of occupation and DebtToIncomeRatio

6.change listing category numeric to string.

Subset of the dataframe by selecting features

### Did you create any new variables from existing variables in the dataset?
Yes, I first created a Datetime variable ‘ListingDateTime’ in format of  ‘yyyy-mm-dd’ to indicate the loan listing date.


## Summary of Findings

**BorrowerState** : The two letter abbreviation of the state of the address of the borrower at the time the Listing was created.

>The Highest BorrowerState is CA (California)

**CountPlots of Number of Loans listed Year, Month and Day**

>It seems like in 2012 & 2013 increase compare to other years January has the highest number of loans listed as expected from starting of new year , whereas april sees the least number of loans listed. There is no difference in number of loans over days and the descrease in 31th day because it only comes six times in a year have the other days.

**DebtToIncomeRatio** : The debt to income ratio of the borrower at the time the credit profile was pulled. This value is Null if the debt to income ratio is not available. This value is capped at 10.01 (any debt to income ratio larger than 1000% will be returned as 1001%).

>Distribution has unimodal peak around 0.2 with unusual peak around 0.25 which indicates most people prefer 1:4 ratio of debt to Income which is a good thing.

**LoanOriginalAmount** : The origination amount of the loan.

>We see that the most freq. amount of loan about 4k also there a multiple peaks at spicific amount 10k, 15k ,20k ,25k ,30k & 35k

**The BorrowerRate** : (interest rate) refers to the annual cost of a loan to  a borrower and is expressed as a percentage. The interest rate does not  include fees charged for the loan. 

**The BorrowerAPR** : is the annual cost of a loan to a borrower. Unlike an interest rate, it includes other charges or fees (such as mortgage  insurance, most closing costs, discount points and loan origination  fees) to reflect the total cost of the loan.

>BorrowerRate should be similar with  slight difference since the APR is always higher than the interest rate.
So that borrower's Annual Percentage Rate greater than Borrower Rate

**Loan Months Since Origination** : Number of months since the loan originated.

>Most loans end up in three periods around 18th , 38th and all end in 60th months period from Originathion.

**ProsperRating (Alpha)** : The Prosper Rating assigned at the time the listing was created between AA - HR.  Applicable for loans originated after July 2009.
>The ratings of most of the borrowers are among D to A with the most of all C. 

**ProsperRating (numeric)** : The  Prosper Rating assigned at the time the listing was created: 0 - N/A, 1 - HR, 2 - E, 3 - D, 4 - C, 5 - B, 6 - A, 7 - AA.  Applicable for loans originated after July 2009.
>It's observed that degree of risk between 4 : 8 It's not good but also not bad which the most common rate is 8

**EmploymentStatus** : The employment status of the borrower at the time they posted the listing.
>Most of borrowers are employed then comes full-time second with a big difference.

### The features you investigated, were there any unusual distributions?

The StatedMonthlyIncome is highly right skewed. To find the outliers that  drive data to the left, I used summary function and find that the maximum  value is 1750000, which is likely to be an error. So in the next plot, I  removed the top 1% data from the original and got a more reasonable plot.

**Stated Monthly Income** : The monthly income the borrower stated at the time the listing was created.

>Most of borrowers are employed then comes full-time second with a big difference.The histogram plot of the original data is highly right skewed. To find the  outliers that drive data to the left, I used describe function and find that  the maximum value is 1750000 which highly affect the result and dose not describe data accurately as 75% is 7000.

> I removed the top 1% data from the original and got a more reasonable plot around 4k.

**Montly Loan Payment ($)** The scheduled monthly loan payment.

>From the histogram I found that most of Prosper loan are less than  1K, indicates the prospers services are mainly on personal loans.

**Listing Category**

ListingCategory	The category of the listing that the borrower selected when posting their listing: 0 - Not Available, 1 - Debt Consolidation, 2 - Home Improvement, 3 - Business, 4 - Personal Loan, 5 - Student Use, 6 - Auto, 7- Other, 8 - Baby&Adoption, 9 - Boat, 10 - Cosmetic Procedure, 11 - Engagement Ring, 12 - Green Loans, 13 - Household Expenses, 14 - Large Purchases, 15 - Medical/Dental, 16 - Motorcycle, 17 - RV, 18 - Taxes, 19 - Vacation, 20 - Wedding Loans

>I found that the most popular services offered by  Prosper are 1-Debt Consolidation, 2-Home Improvement, 7-Other and 3-Business.

**Term, Income Range, Loan Status**

**Term : The length of the loan expressed in months.**
>Most loans are 36 month terms in this dataset.

**IncomeRange : The income range of the borrower at the time the listing was created.**
>Borrowers' income are mostly below 75,000$ per year.

**LoanStatus : The current status of the loan: Cancelled,  Chargedoff, Completed, Current, Defaulted, FinalPaymentInProgress, PastDue. The PastDue status will be accompanied by a delinquency bucket.**
>Most loans are in these current days or completed.

**Occupation** : is the occupation selected by the Borrower at the time they  created the listing.

>We dicoverd that the top five  occupations counts are Other, Professtional, computer programmer, Excutives and Teacher.

**Is Borrower Home Owner** : A Borrower will be classified as a homowner if they have a mortgage on their credit profile or provide documentation confirming they are a homeowner.

>it shows 53% do own a home & 47& do not own one.

**The Correlation Matrix and Regression Plot Shows Correlation between multiple features.**

>LoanOriginalAmount and MothlyLoanPayment, PorsperScore, Term, Investors, CreaditScoreRangeLower, Year.
Year and LoanMonthlysinceOrigination, Term, MothlyLoanPayment.

>BorrowerAPR and PorsperScore, MothlyLoanPayment, BorrowerRate, CreaditScoreRangeLower, AvailableBankcardCreadit, LoanOriginalAmount.

>BorrowerRate and PorsperScore, MothlyLoanPayment, CreaditScoreRangeLower, AvailableBankcardCreadit, LoanOriginalAmount.

>MothlyLoanPayment and Investors.

**Time vs Borrower Rate**

>We Choose to plot borrower rate with month over years To reduce the noises & Months over all. Now the  plot shows clearly how interest rates changed over time. However, there’s no  obvious seasonal fluctuation or monotonic behaviors. Time may not be a good  independent variable to predict the borrower’s interest rate.

**AvailableBankcardCredit vs. BorrowerRate**

AvailableBankcardCredit : is total available credit via bank card.  It can be an indicator of a borrower’s credit history.

>A reasonable guess is that a higher available bank card credit will lower  your interest rate. This guess is proved to be true from following plot.  The points are clustered at the bottom left corner, when a borrower has  relatively low credit amount (<25,000) the probabilities of getting low  and high interest rates are similar. However, when the borrower’s credit  amount is high (>50,000), he/she is more likely to get a lower interest rate.

**BorrowerAPR vs LoanOriginalAmount**

>This plot shows that at different size of the loan amount, the APR has a large range, but the range of APR decrease with the increase of loan amount. Overall, the borrower APR is negatively correlated with loan amount. 

**Occupation vs BorrowerAPR, MonthlyLoanPayment, LoanOriginalAmount, DebtToIncomeRatio.**

**Borrower APR vs Occupation**
>The borrower APR changes with the occupation,Interestingly with student in technical schools having least and college sophomores having highest average rating.

**MonthlyLoanPayment vs. Occupations**
>The top 3 occupations have high monthly loan payment are Judge, Doctor,  and Pharmacist. 

**LoanOriginalAmount vs. Occupations**
>Also The higest Occupation with Montly loan payment are with The highest loan Original Amount .The Loan Originak Amopunt should be positively correlated  with the monthly loan payment. The plot is consistent with salaries of each occupation.

**Salary (StatedMontlyPayment) vs Occupation**
>The Top 6 Occupation in there average Salary are Doctor, Attorney, Excecutive, Dentist and Pharmacist. The plot is consistent and positively correlated with The Loan Original and the monthly loan payment. of each occupation. 

**Occupation vs ProsperRating (Alpha)**

>The Occupation with the top salary like Doctor, Judge, Executive, Attorney, Dentist have a comman top Rate which is A Rated, The most comman top Rate in most Occupation is C Rate.

**EmploymentStatus vs ProsperRating (Alpha), Term**

>Interestingly, it appears that there are some positive relationships between the categorical variables and the two numeric variables of interest. The loans with 60-month term loans were quite popular with those with a ProsperRating of A and C. As seen before 36-month term loans are the most popular across all credit risk groups.

**The stated monthly income changes for different loan Terms when split up by ProsperRating (Alpha)**

>The stated monthly income change with the increase in the borrow term and ratings on an average.

**Loan original amount changes for different loan Terms when split up by ProsperRating (Alpha)**

>But for the loan amount, there is an interaction between term and rating. We can see that with a better Prosper rating, the loan amount of all three terms increases, the increased amplitude of loan amount between terms also becomes larger.

**The Borrower APR changes for different loan Terms when split up by ProsperRating (Alpha)**

>Interestingly, the borrower APR decreases with the increase of borrow term for people with HR & C ratings. But for people with B & AA ratings, the APR increase with the increase of borrow term.

**The BorrowerRate changes for different loan Terms when split up by ProsperRating (Alpha)**

>This seems to not make sense but for every single level of the ProsperRating, the BorrowerRate increases as for longer-term loans. I would think it to be the reverse as shorter-term loans usually carry a higher interest rate. This was not at all evident in the bivariate analysis and comes a bit as a surprise.

**Stated monthly income**
>it doesn't seem like there is a interaction effect between term and rating, the pattern of term is similar among different ratings. But for loan amount, there is a interaction between term and rating. We can see that with better Prosper rating, the loan amount of all three terms increases, the increase amplitude of loan amount between terms also becomes larger.

**Interest Rate vs. Time vs. Catagory**

**ListingCategory**	The category of the listing that the borrower selected when posting their listing: 0 - Not Available, 1 - Debt Consolidation, 2 - Home Improvement, 3 - Business, 4 - Personal Loan, 5 - Student Use, 6 - Auto, 7- Other, 8 - Baby&Adoption, 9 - Boat, 10 - Cosmetic Procedure, 11 - Engagement Ring, 12 - Green Loans, 13 - Household Expenses, 14 - Large Purchases, 15 - Medical/Dental, 16 - Motorcycle, 17 - RV, 18 - Taxes, 19 - Vacation, 20 - Wedding Loans

>From the time series plot in last section, I didn’t get useful information  about how the interest rate changes with time. So I included another  variable (listing catagory) here to see if we can find any interesting  trend for individual listings.

>The lines for each catagory are similar with the mean plot except one huge  jump for the auto loan in year 2009. But when look back to the first time  series plot, I found there’s only a few data point within that time window.  Thus any outlier was able to drive the line up.

## Key Insights for Presentation

### However did the feature(s) of interest vary with alternative features within the dataset?

The borrower Annual percentage rate is negatively related to the loan original amount, that mean the additional the loan amount, the lower the Annual percentage rate. It additionally shows that at totally different size of the loan amount, the Annual percentage rate contains a higher range, however the range of Annual percentage rate decrease with the rise of loan amount. The Prosper rating additionally contains a huge impact on the receiver Annual percentage rate, that decreases with the higher rating.

### Did you observe any fascinating relationships between the opposite features (not the most feature(s) of interest)?

The loan original amount is positively related with the explicit monthly income, it is sensible since borrowers with additional monthly income may loan more cash. It additionally shows that borrowers with higher rating even have larger monthly income and loan amount. there's a interaction between prosper rating and term. proportionately, there are additional sixty month loans on B and C ratings. there's solely thirty six months loans for hr rating borrowers.

### Were there features that strengthened each other in terms of looking at your feature(s) of interest?

I extended my investigation of borrower APR against loan amount by looking at the impact of the Prosper rating. The multivariate exploration showed that the relationship between borrower APR and loan amount turns from negative to slightly positive when the Prosper ratings increased from HR to AA. I then explored the rating and term effects on loan amount, it shows that with better Prosper rating, the loan amount of all three terms increases, the increase amplitude of loan amount between terms also becomes larger. 

### Were there any interesting or surprising interactions between features?

A surprising interaction is that the borrower APR and loan amount is negatively correlated when the Prosper ratings are from HR to B, but the correlation is turned to be positive when the ratings are A and AA. Another interesting thing is that the borrower APR decrease with the increase of borrow term for people with HR-C raings. But for people with B-AA ratings, the APR increase with the borrow term.

## Limitations
The Exploratory Data Analysis is a good way to know the data using vivid and interesting visualizations. However, to make final statement about the  relationships among variables we need to conduct statistical test and  build predictive models.
