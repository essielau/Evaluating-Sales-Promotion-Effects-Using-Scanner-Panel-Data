BUMK758K: Advanced Marketing Analytics


Project #3: Evaluating Sales Promotion Effects Using Scanner Panel Data


General Instructions on the Project Memo:

1.	Please include a cover page with the title of the project, name of your group (A, B, C, … etc.), and each group member’s name. Please also include the honor pledge.   

2.	The main text of the memo should be no more than 2 pages, single-spaced.  In addition, you can include a number of tables and figures in the appendices. There is no strict limit on the number of appendices, but please include only the essential information necessary to support your analysis.

3.	Please refer to the document “Project Memo Template” for the format and suggested contents of the memo. This file is posted on Canvas. 

4.	You should work with only members in your own group for the assignment.

5.	This assignment is due at the beginning of the next computer class. Please submit a hard copy of your memo.



Background

Sales promotions are short-term incentives given to consumers, channel distributors, or a company’s own sales force in order to increase sales of a product. Sales promotions consist of a variety of incentives aimed at stimulating quick responses and more purchases in the short run. A particular sales promotion activity lasts for only a limited time period (usually a few days to several weeks). Sales promotions can often be implemented quickly and get sales results sooner than advertising. For retailers, the most important consumer sales promotion tools are temporary price cuts, in-store displays (store front, end-of-aisle, etc.), feature advertising (also called “free standing inserts”), and coupons. These incentive promotions are used to attract new buyers, to reward existing buyers, to entice brand switching, or to stimulate greater purchase quantities. Consumer packaged goods (CPG) companies are the biggest spenders on sales promotions. Total sales promotion expenditure is about twice as much as total advertising spending in the US, and it is also growing at a faster pace than advertising expenditure. In some CPG companies, sales promotions account for as much as 60-70% of the total marketing budget. The effectiveness of sales promotions can be assessed using store-level aggregated sales data or individual household level scanner panel data. In this project, we use household scanner panel to assess the effectiveness of sales promotions on individual consumers’ purchase behavior, specifically, in terms of their category purchase incidence, brand choice, and purchase quantity decisions.

The main objectives of this assignment are two-fold: to analyze sales promotion effects using household scanner panel data, and to assess the profitability of sales promotions based on the model estimation results.  

Data Description

In this assignment, we use scanner panel data of liquid laundry detergent provided by Information Resources, Inc. (IRI). The raw data have been preprocessed to serve the purposes of this exercise. The specific dataset used here includes liquid laundry detergent purchases made by 178 households from four stores in a mid-west market during a 135-week period. The four stores belonged to the same supermarket chain and were located in close proximity. They had the same pricing and promotion activities for the category under investigation. Only the top four selling brands were included to simplify the analysis. Different sizes and variants of a brand were combined and treated as one choice alternative. The four brands are: 1 = Wisk; 2 = All; 3 = Tide; 4 = Cheer. Wisk and All are Unilever brands, and Tide and Cheer are Procter & Gamble brands.        

	Two SAS data files are provided for your analyses. The following is a description of the contents and variables included in each file.

“deterg.sas7bdat”: This is the complete dataset with information on household purchase incidence, brand choice, and purchase quantity, as well as price and promotion for each brand in a given week.  There are 19157 observations in this file.

“choice_det.sas7bdat”: This dataset is needed for estimating brand choice models using SAS procedure “PROC MDC”. It was created by selecting those observations in “deterg.sas7bdat” where a category purchase incidence occurred (i.e., INCID=1). Note that PROC MDC requires a special data structure in which K rows are needed to describe one brand choice occasion, where K is the number of brands in the choice set (K = 4 here).  There are 781 choice occasions and therefore 3124 observations in this file.

The variables are described in the following two tables.

Variables in “deterg.sas7bdat”
Variable
Definition
PANID
An 8-digit ID number for a household in the IRI panel.
WEEK
A numerical number representing the week according to IRI’s system.  (It ranges from 906 to 1040 in the data. week 906 refers to Jan. 6-12, 97)
INCID
= 1 if a household makes a category purchase in a given week; = 0 otherwise
CHOICE
= 0 if no category purchase incidence; = 1 if Wisk is chosen; = 2 if All is chosen; = 3 if Tide is chosen; = 4 if Cheer is chosen.
LCHOICE
Brand choice made on the previous category purchase occasion. Same coding as CHOICE.
VOLUME
Purchase quantity of the chosen brand, measured in ounces.
REGPR1
Regular price for Wisk in a given week, measured in cents/ounce.
REGPR2
Regular price for All in a given week, measured in cents/ounce.
REGPR3
Regular price for Tide in a given week, measured in cents/ounce.
REGPR4
Regular price for Cheer in a given week, measured in cents/ounce.
PCUT1
Amount of price cut for Wisk in a given week, measured in cents/ounce.
PCUT2
Amount of price cut for All in a given week, measured in cents/ounce.
PCUT3
Amount of price cut for Tide in a given week, measured in cents/ounce.
PCUT4
Amount of price cut for Cheer in a given week, measured in cents/ounce.
DISP1
= 1 if Wisk has an in-store display promotion in a given week; = 0 otherwise 
DISP2
= 1 if All has an in-store display promotion in a given week; = 0 otherwise 
DISP3
= 1 if Tide has an in-store display promotion in a given week; = 0 otherwise 
DISP4
= 1 if Cheer has an in-store display promotion in a given week; = 0 otherwise 
FEAT1
= 1 if Wisk has a feature ad promotion in a given week; = 0 otherwise
FEAT2
= 1 if All has a feature ad promotion in a given week; = 0 otherwise
FEAT3
= 1 if Tide has a feature ad promotion in a given week; = 0 otherwise
FEAT4
= 1 if Cheer has a feature ad promotion in a given week; = 0 otherwise
LBPROMOT
= 1 if the previous category purchase was made on promotion; = 0 otherwise
AVOL
A household’s average purchase quantity in a previous period, in ounces.


Variables in “choice_det.sas7bdat”
Variable
Definition
CASEID
An ID number for each choice occasion.
PANID
An 8-digit ID number for a household in the IRI panel.
WEEK
A numerical number representing the week according to IRI’s system.  (It ranges from 906 to 1040 in the data.)
BRAND
1 = Wisk; 2 = All; 3 = Tide; 4  = Cheer
DECISION
1 = the brand (as indicated by BRAND) is chosen; 0 = otherwise
REGPR
Regular price for the brand (as indicated by BRAND), in cents/ounce.
PCUT
Amount of price cut for the brand (as indicated by BRAND), in cents/ounce.
DISP
1 = there was an in-store display promotion for the brand (as indicated by BRAND); 0 = otherwise 
FEAT
1 = there as a feature advertising promotion (i.e., Free Standing Insert) for the brand (as indicated by BRAND); 0 = otherwise

Assignment:

The learning objective of this assignment is to learn how to estimate models of category purchase incidence, brand choice, and purchase quantity in SAS, and to understand how to use the model estimation results to assess sales promotion effects. Therefore, the emphasis is on how to interpret the outputs from the software.

You are provided with an EXCEL file “promotion_effects.xlsx” which contains a template for estimating the 1) category purchase incidence probability, 2) brand choice probabilities, 3) conditional purchase quantity, and 4) total sales effects of any promotions using estimation results from the sample program. I recommend you to study this file before doing your own analyses. Most analyses you need to conduct for the assignment can be done by modifying the sample template.

You are given the regular price for each brand in week t, in cents/ounce: (they are the average values in the data)

REGPR1 (Wisk) = 7.18		REGPR2 (All) = 4.59
REGPR3 (Tide) = 7.29 		REGPR4 (Cheer) = 6.54

Note that these are unit prices aggregated across different package sizes for a brand. To make the interpretation more tangible, you can convert them to equivalent prices measured as “$/bottle for a 100-ounce bottle”.  For example, the equivalent regular price for Wisk is $7.18 for a 100-ounce bottle. The same applies to price discounts.

Assume that if a price discount is to be offered for a brand, the amount of price cut takes the average value in the data (i.e., the average over items that were sold at a discount). The average values were (in cents/ounce): Wisk = 0.70; All = 0.82; Tide = 0.97; Cheer = 0.65. 

To simplify your analysis, assume that only one brand in the category is promoted in a given week, if any. In addition, assume LBPROMOT=0.  


Your memo should address (but not be limited to) the following issues.

1.	How effective are the three types of sales promotions (price discount, in-store display, and feature advertising) in influencing consumers’ purchase incidence, brand choice, and purchase quantity decisions for the laundry detergent category?  

2.	Which one of the three types of promotions, when offered alone, appears to generate the greatest expected sale quantity increase for the brand Wisk (brand 1 in the data) among the 178 households in the data?

3.	What are the effects of combining multiple sales promotion vehicles for a given brand, and which combination is most effective in stimulating sales? You can use just Wisk (brand 1) to illustrate the analysis and results.

4.	Now relax the assumption that the retailer promotes only one brand in the category, if any, in a given week. Explore the impact of promoting two (or more) brands simultaneously on category purchase incidence probability, brand choice probabilities, brand-specific sales quantities, and the total category sales quantities.

Based on the above analyses, what recommendations would you make to the retailer with regard to its sales promotion planning and executions for the laundry detergent category? 


Hint for Q2 and Q3:

You first need to predict the expected purchase quantity in week t for Wisk for each household based on the model estimation results for four scenarios: without any promotions, and with one of the three promotions for Wisk at a time. And then, take the sum over the 178 households.  

Expected purchase quantity = Pr(incidence)*Pr(brand choice)*Conditional purchase quantity given that a brand is chosen.

Note that the expected purchase quantity in one week from 178 households is very small in magnitude due to the low purchase frequency of the category. The percentage change is a more meaningful measure to reflect the effects of sales promotions. 

The variables you need for estimating the expected purchase quantities are available in the Excel file “promotion_effects.xlsx”. Note that there are no household-specific variables used in our purchase incidence and brand choice models. Therefore, one can estimate the incidence and choice probabilities first, and then combine them with the household-specific conditional purchase quantities.
