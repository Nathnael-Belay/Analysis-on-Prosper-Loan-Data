# Exploration of Loan Data from Prosper
## by Nathnael Belay


## Dataset

> This exploration is based on a list of loans gathered from a peer-to-peer loan market place called Prosper. The data set contains 113,937 loans with 81 variables on each loan, including loan amount, borrower rate (or interest rate), current loan status, borrower income, and many others. For the purpose of this exploration, only a subset of the variables thought to give better insight were used. Preliminary wrangling efforts were also applied on top of subsetting the variables, were missing values, outliers and incorrect data types were handled as well as new features derived.

> The original dataset can be found [here](https://www.google.com/url?q=https://s3.amazonaws.com/udacity-hosted-downloads/ud651/prosperLoanData.csv&sa=D&ust=1581581520570000) for download. And the data dictionary [here](https://www.google.com/url?q=https://docs.google.com/spreadsheet/ccc?key%3D0AllIqIyvWZdadDd5NTlqZ1pBMHlsUjdrOTZHaVBuSlE%26usp%3Dsharing&sa=D&ust=1554486256024000)


## Summary of Findings

> Preliminary wrangling effors were taken to better prepare the data for analysis. Durining the process, unwanted columns were dropped, column names were corrected to fit the convention to a certain extent, data types were corrected, missing values were handled and two new columns were derived to assist the exploration process.

> ListingToLoanOriginationInDays column was derived by extracting the date difference in days of LoanOriginationDate and ListingCreationDate, to depict the wait period in days for a listing before a loan grant.

> DeliquencyRate column was also derived by dividing the DeliquenciesLast7Years columns with TotalCreditLinesLast7years to have a more meaningful attribute than the two separately would.

> The cleaned dataset then resulted with a structure of 84984 rows and 23 columns.

> LoanStatus, BorrowerAPR, ProsperRating_numeric and ListingToLoanOriginationInDays were initially identified to be the main focus of the exploration with Term, BorrowerRate, ListingCategory, EmploymentStatus, EmploymentStatusDuration, IsBorrowerHomeowner, DelinquencyRate, DebtToIncomeRatio, IncomeRange, IncomeVerifiable, StatedMonthlyIncome, LoanOriginalAmount and MonthlyLoanPayment expected to give supporting insight.

> There was an outlier value in the ProsperScore variable, which I corrected after a careful inspection of what it could have been meant to be. A normal distribution was observed after that, with the most scores ranging between the value of 4 to 8.

> The distribution of ProsperRating_numeric looked normal, with the most ratings ranging from the value of 3 to 6.

> Majority of the loan statuses were observed to be of the 'Current' category with the 'Completed' status coming second with more than half the count of the 'Current' status. Loans defaults and late payments were found to be relatively rare. Due to this fact, I decided to not use this attribute further. Since the low number of data points for the negative statuses will not be enough to give significant indication to my question of what might lead to loan defaults and/or late payments.

> The distribution of BorrowerAPR looked fairly normal with one exceptional peak around the value of 0.35.

> The wait days attribute, ListingToLoanOriginationInDays, also had a right skewed distribution. After applying log scale and x-axis limit operations, wait days were observed to mostly fall under the 1-30 days range.

> I have used Scaling and Transformation operations, such as the log scale and x-axis limit restrictions, on 'StatedMonthlyIncome','DebtToIncomeRatio', 'MonthlyLoanPayment' and 'EmploymentStatusDuration' variables as the distribution was heavily skewed with a long tail in the right direction.

> While investigating further the StatedMonthlyIncome attribute, I found out that a few outliers with a value greater than 40000 are causing the exaggerated tail on the distribution chart. Having that in mind, I decided to look at the subset of the dataset with StatedMonthlyIncome value below 40000 on the log scale to generate better insight.

> I also followed the same approach for the 'DebtToIncome' variable, where the data was skewed to the right with few data points above the value of 2 dragging the tail. I zoomed in on the data with limiting the x-axis at the value of 2, took a subset of the data then checked the distribution on the log scale.

> The distribution of LoanOriginalAmount had to also be viewed on the log scale to generate better insight and it indicated there to be commonly borrowed amounts. The most common being 4000, 1000 and 15000.

> To my surprise, there was no indication that the ProsperScore and ProsperRating attributes had any impact on the ListingToLoanOriginationInDays, which is basically the days a borrower had to wait before getting the desired loan, despite my expectations. I expected lower ratings would somehow result in longer wait time since lenders would be reluctant to lend. I was also surprised to not have found meaningful correlation between the categorical variables and the ListingToLoanOriginationInDays attribute.

> BorrowerAPR has also shown strong correlations with most of the variables. Having strong negative correlations with ProsperRating, LoanOriginalAmount and MonthlyLoanPayment, which makes sense. It also has slightly positive correlations with DelinquencyRate and DebtToIncomeRatio. The relationship between Term and BorrowerAPR was also analysed but a conclusive correlation between the two attributes could not be deduced.

> DelinquencyRate defined as the NumberOfDelinquencies devided by TotalNumberOfLoansTaken, has been observed to have a negative impact on ProsperRating while having a positive correlation with BorrowerAPR and BorrowerRate, both as expected. It also has a slight negative correlation with LoanOriginalAmount and MonthlyLoanPayment.

> LoanOriginalAmount and MonthlyLoanAmount appear to positively impact the ProsperRating of a loan lising. While DelinquencyRate and DebtToIncomeRatio display a negative impact on the ratings.

> IncomeRange had a positive impact on both ProsperRating and BorrowerAPR. Higher ProsperRatings were observed for income ranges on the higher scale, and lower annual percentage rates were awarded to the higher income ranges.

> An interesting relationship was observed amongst LoanOriginationAmount, ProsperRating and BorrowerAPR. Loan Amount and Prosper Rating had a positive correlation where an increase in one also correlated with an increase in the other. Prosper Rating and BorrowerAPR also had significant negative correlation where a higher rating meant a lower APR, which is good. Loan Amount starts to show an increase as BorrowerAPR starts to decrease and peaks around the BorrowerAPR value of 0.1 - 0.2, then shows a slight decrease for BorrowerAPR < 0.1.

> BorrowerAPR decreases as IncomeRange get higher. While LoanOriginalAmount and ProsperRating increase along with an increase in IncomeRange.

> A Postive correlation between Term and LoanOriginalAmount was observed. Loan Amounts increased as the loan term increased. The majority of the loan amounts were relatively higher for the 60months term.


## Key Insights for Presentation

> The most common listing category was found to be 'Debt Consolidation'.

> 91.36% of loan seekers had a verifiable Income.

> BorrowerAPR and ProsperRating were found to have the highest correlation with a score of -0.96. Where a decrease in the rating resulted in an increase in the annual performace rate, and vice versa.

> A significant negative correlation between LoanOriginalAmount and BorrowerAPR was also observed. Which can be explained by the need of lenders to get an acceptable return on their investment. The lower the loan amount the higher the rate would have to be for them to get a decent incentive to lend.

> IncomeRange was found to positively impact ProsperRating and Loan Amount of a listing, where higher income ranges benefited higher ratings and amounts. While it negatively correlated with BorrowerAPR, where the BorrowerAPR tended to decrease noticeably as the IncomeRange gets hiigher.