### Pandemic-Exacerbated Redlining? An Investigation into Ohio Mortgage Approvals
### Final Project

#### Introduction

The rise of automation in residential real estate is a double-edged sword.  On one hand, it has boosted the popularity of online real estate marketplaces like Zillow, allowing millions of people to easily estimate home values for free. Meanwhile, the opacity of algorithms can make it more difficult to uncover insidious practices like redlining, wherein financial institutions restrict access to mortgages and favorable interest rates based on race.  In August 2021, news outlet The Markup released an investigation where loan applicants of color were 40% to 80% more likely to be denied mortgages in 2019 compared to White applicants with similar credentials .  Their findings led them to conclude that there was evidence of redlining in ostensibly unbiased automated decision-making in mortgage approvals. In reading their report, I became interested in understanding how the pandemic affected racial disparities in mortgage approval rates for single-family homes, which exploded in demand during 2020 stay-at-home orders as people wanted more space.

Accordingly, I will investigate whether the pandemic has exacerbated differences in mortgage approval rates between non-White and White applicants in Ohio single-family housing neighborhoods between 2018 and 2020, to investigate trends in redlining. I constrained my analysis to the state of Ohio as several of its regions observed some of the highest municipal housing price growth in the US over the pandemic and it has a relatively even split between state-wide White vs minority populations.

#### Description of Data Set and Variables

This study’s primary data will come from three separate files: the Home Mortgage Disclosure Act’s (HMDA’s) Dynamic National Loan-Level Data Set for the calendar years of 2018, 2019, and 2020. This data is the entire population of mortgage applications submitted in that specific year in the United States, a required disclosure by lenders as part of the Dodd-Frank Act.  Accordingly, this is a complete and representative sample of US mortgage submissions.  From the original 99 features in the data set, I narrow it down to 12 independent variables and one dependent variable; my reasoning is described in the subsequent section.

From the original data set, I filtered my data to Ohio single-family property applications and used only applications whose “Loan Purpose” was equal to 1 so that my subset pertains exclusively to mortgages for home purchases rather than other purposes such as re-financings or home improvement since my research question relates to redlining. Among Ohio single-family housing mortgage applications where I have approval/denial data and where I am not missing applicants’ self-reported race, I have 161,644 data points remaining in the 2020 data set, 153,605 in the 2019 data set, and 342,482 in the 2018 data.  However, I acknowledge that my scope and data quality issues pertaining to my intended analysis filters out about 65% of my original data, but it also makes it more manageable to process for this analysis.

It is crucial to acknowledge that a key variable is missing from this data set: applicants’ credit scores.  Credit scores are a widely used metric to determine how people access credit, but the confidential nature of this information means we cannot incorporate it into our analysis or accurately approximate it without making some strong assumptions.

As an aside, I had planned to constrict my analysis to Ohio neighborhoods with above-average property growth in 2020 by incorporating property value growth information from the American Community Survey (ACS), but 2020 ACS median property values are not yet available by county at the time of this paper so I have gone forward with the entire population of Ohio single-family homes.

On a different note, some notable outliers, likely driven by data quality issues, in the original data set were subsequently removed from this analysis.  Where there were null values or codes that represented null values in my independent and dependent variables (as long as the variable did not pertain to an optional co-applicant), I decided to remove them from my analysis.  Since my study involves the population of mortgage applications, I deemed the removal of applications with null values to be a reasonable reduction in my sample size. Data quality issues and concerning outliers were evident in the wide standard deviations that I noticed in my exploratory data analysis and unintuitive values (for instance, it is unlikely that people requested over 1,000 months for mortgage repayment). 

To address data quality issues or extreme outliers, the following changes were made:

*	Property value cannot be null and must not be larger than $10,000,000
*	Loan term must be less than 999 months
*	The combined loan to value ratio cannot exceed 1,000 times the value
*	Applicant age cannot be greater than 100
*	Income greater than $5 million
*	Income less than $0 

Overall, the removal of null values and outliers refined my data set to 423,080 data points.  A next step outside the scope of this study would involve verifying that the excluded data points follow the population distribution, avoiding unintended bias in covariates.
 
#### Dependent Variable

1.	action_taken: This variable indicates mortgage denial vs approval and originally has 8 possible values.  I recoded the original values 1 (loan originated/approved) and 2 (approved, but not accepted) to the dummy variable of “1”, indicating that the mortgage was approved.  The original value “3” will be recoded as “0”, indicating that the mortgage was denied.  All other values will be filtered out of the data set, because they don’t indicate a final approval outcome as the application was withdrawn, closed for incompleteness, or was a preapproval application.

Among my remaining data points, my sample is imbalanced as 93% of applications were approved and only 7% were rejected (Table 1).  This makes sense as the mortgage application process is rigorous and applicants would only complete it if they were serious about buying a home.  Accordingly, people must have confidence in the strength of their application to even submit one.
 
Table 1. Distribution of Binary Dependent Variable “action_taken”

action_taken	 Count
0 (rejected)	29,138 (7%)
1 (approved)	393,942 (93%)

#### Independent Variables

With 98 independent variables, this study incorporated only 12 of them.  In part to manage the complexity of the analysis, they were also chosen by a general understanding of the financial considerations involved in mortgage applications as well as control variables that might inform any findings around discrimination.

1.	activity_year: Used as a dummy control variable, this indicates the year (between 2018 to 2020) that the mortgage application was successfully and fully submitted.  This is considered a categorical factor variable for my analysis.  I hypothesize that there is no relationship between year and likelihood of mortgage approval, because there were no policy changes in the past three years that would alter mortgage approval decision-making.

2.	applicant_age: This is a categorical variable indicating the age of the applicant with ranges such as “<25”, “25-34”, and “>74”, which I will transform into an ordinal variable with the scale of 1 (the youngest age group) to 7 (the oldest age group). I hypothesize that older age groups have a higher likelihood of application approval as older applicants have greater accumulated wealth and income than younger applicants.

3.	applicant_race_1: Self-reported categorical variable according to a list of 18 options.  While the data set allows applicants to give five (5) different responses to race, I consider the first entry as the primary race, especially since it has the fewest null values.  I recoded this variable into a dummy variable for White = 0 and non-White = 1.  I assume that this will be a statistically significant dummy control variable and that non-White applicants are less likely to receive mortgage approval even though this is a legally protected trait.

4.	applicant_sex: Categorical variable indicating the self-reported sex of the applicant. 1 (male) and 2 (female) will remain in the data set. However, the values of 3 and 4 were removed from the data set since it denotes that a sex was not disclosed; the value of 5 does not exist for this variable.  The value of 6 (applicant selected both male and female on application) will be recoded as 3.  I view this variable as a dummy control and hypothesize that it should have no relationship to mortgage approval outcomes since this is a protected trait.

5.	co_applicant_exists: While my data set has co-applicant characteristics such as age, race, and sex, I decided to create a dummy variable to represent whether a co-applicant is on the application or not.  Since the inclusion of a co-applicant is optional, I decided to use a binary variable to bypass the k null data.  I hypothesize that the existence of a co-applicant increases the likelihood of mortgage approval, since this improves key financial metrics like income and debt-to-income, ultimately lowering the applicants’ lending risk.

6.	combined_loan_to_value_ratio: The ratio of the total mortgage secured by the property compared to the value of the property. This variable incorporates the applicant’s proposed down payment, which would reduce this ratio.  Accordingly, I hypothesize that the relationship is negative: a lower combined loan-to-value ratio raises the likelihood of mortgage approval, that this will be highly statistically significant and the magnitude of change will be large.

7.	debt_to_income_ratio: This (quasi-continuous) numeric variable measures an applicant’s risk of defaulting on the mortgage and their ability to make debt repayments since it considers their monthly debt (with the mortgage included) to their monthly income.  I hypothesize that a lower debt-to-income ratio should increase the likelihood of mortgage approval, and that this will be highly statistically significant.

In terms of recoding, this variable is particularly complex as the data lists the actual debt-to-income ratio value if it falls between 36% and 50%; any other value is listed as a range such as “<20%” or “50% - 60%”.  I recoded this variable as an ordinal categorical variable where 36% to 42% inclusive is its own range, and 43% to 49% inclusive is another.

8.	ffiec_msa_md_median_family_income: The median family income in the census tract where this property is located.  I include this variable to help control for the “desirability” or wealth of a neighborhood and hypothesize that there is a positive relationship between a community’s median family income and mortgage approval.  Since affluent neighborhoods attract other affluent prospective buyers, these applicants likely have the favorable financial resources and profiles to move into these areas without mortgage application difficulties.

9.	income: The gross annual income of the applicant and if applicable, combined with the co-applicant’s gross annual income. This continuous numeric variable was log transformed due to the wide range in values.  I hypothesize that as income increases, the likelihood of mortgage approval increases, this will be highly statistically significant, and the magnitude will be large.

10.	loan_amount: This continuous numeric variable is the mortgage loan amount in US dollars requested in the application. This variable was log-transformed in my analysis. I hypothesize that the relationship is quadratic for loan amount, as extremely large loans may be seen as too risky, while very small loans likely stem from first-time or low-income buyers who do not have a credit history of takin.  I believe this will be highly statistically significant with a large magnitude, because this is tied closely to risk, about which lenders are very concerned.

11.	property_value: This continuous numeric variable is the value of the property in US dollars; it was log transformed in my analysis. I hypothesize that greater property values are more likely to be approved for a mortgage, because applicants attempting to purchase more valuable homes likely have sufficient existing assets and wealth and are trying to upgrade.  Estimating a quadratic relationship, I hypothesis that this variable will be moderately statistically significant or may be insignificant.

12.	tract_to_msa_income_percentage: This continuous numeric variable is the percentage difference in income between the specific census tract where the property is situated and the metropolitan statistical area (MSA).  In other words, it’s a proxy for how affluent or impoverished a community may be compared to the metropolitan area to which it belongs.  I include this variable as a control and hypothesize that it will be statistically significant since my hypothesis involves the presence of redlining.
