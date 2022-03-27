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
