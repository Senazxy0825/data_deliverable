# tech report
How many data points are there in total?
Our full dataset has 1485961 entries in total, we also have a final truncated version with only 5000 entries. With so many entries, even if we split by state, this is without a doubt enough entries for hypothesis testing as well as validating our results.

What are the identifying attributes?
A combination of bed, bath, acre_lot, city, state, house_size, and zip_code can reasonably be used to discern houses from each other. A house having the exact same size and number of bedrooms and bathrooms in the same city and zip code is not terribly likely. In the rare case where there may be two unique houses with all those being the same, we can use price as well to help discern duplicates from uniques, though using price is not ideal since price is constantly fluctuating and we may have two entries for the same house from different times, with different prices.

Where is the data from?
The data comes from multiple sources, including Kaggle (which contains real estate listings scraped from realtor.com), Zillow (for housing affordability data), and the Tax Foundation (for property tax data by state and county).

How did you collect your data?
The data was collected from publicly available datasets. The primary dataset was sourced from Kaggle, which had already been scraped from realtor.com. Additional datasets were obtained from the Tax Foundation and Zillow’s research data portal.

Is the source reputable?
Yes, the sources are reputable. Realtor.com is a well-known real estate platform, Zillow is a widely used housing market analysis tool, and the Tax Foundation is a well-regarded policy research organization. These sources provide reliable data that is commonly used in real estate analysis.

How did you generate the sample? Is it comparably small or large? Is it representative or is it likely to exhibit some kind of sampling bias?
We randomly sampled 100 data points to use in our analysis. The sample size is relatively small, which may not fully capture all real estate trends within 50 states. Potential biases : 1. If the random sample includes more samples from one state instead of another, it may not fully reflect the diversity of the state's housing market. 2. The real estate dataset is updated weekly, but we are using a fixed dataset, so it may not fully reflect recent market changes. 3. Zillow’s affordability data assumes a 20% down payment and 30% income-to-housing cost ratio, which may not represent all homebuyers' financial situations.

Are there any other considerations you took into account when collecting your data?
The real estate dataset is claimed to be updated weekly on Zillow, meaning some properties may be over- or underrepresented depending on market activity. The state tax dataset is for 2023, while Zillow’s affordability data is reported monthly. To maintain consistency, we averaged Zillow’s affordability data over 12 months of 2023 before merging it into the dataset. The dataset is limited to 100 random samples from each of 50 states, so it may not reflect the whole situation. 

How clean is the data? 
How did you check for the cleanliness of your data? What was your threshold reference?
We have used methods like .info() and .describe() to check data types, ranges, and exceptions to ensure that the values in the critical fields remain consistent. We checked for data cleanliness by ensuring that the prev_sold_date field contained valid dates and filtering out records beyond a certain threshold. The cutoff_date = pd.Timestamp('2025-03-14') was used as a reference to exclude any future or incorrect values. By setting the cutoff date, we ensured that only relevant historical data was retained. 

Did you implement any mechanism to clean your data? If so, what did you do?
We have implemented mechanisms such as dropping duplicates, processing missing values through imputation (or removal), and converting data types to standardize. We handled missing values by either imputing them or removing incomplete records to maintain consistency. The prev_sold_date column was converted into a standardized datetime format to avoid inconsistencies. Additionally, we applied a filtering condition to remove records beyond 2025-03-14 and randomly sampled 100 entries per state to keep the dataset at a manageable size. This random sampling preserved meaningful variables like income and tax, ensuring that our dataset remained representative and analytically useful.

Are there missing values? Do these occur in fields that are important for your project's goals?
There were some missing values such as acre_lot (the piece of land that is measured in acres), but they were in non-critical fields or were managed by estimation in important fields to maintain the data integrity.

Are there duplicates? Do these occur in fields that are important for your project's goals?
No, there are no duplicates in our current dataset. 

How is the data distributed? Is it uniform or skewed? Are there outliers? What are the min/max values? (focus on the fields that are most relevant to your project goals)
Overall, the data is relatively uniform, slightly skewed towards smaller houses (house_size). There are, on average, more houses around the two to five thousand area for size, with a sharp dropoff for houses that are larger than those. Among the smaller houses around the average, the houses are distributed relatively according to house_size. There are some outliers though, with one significant outlier having a house_size equal to 247421, which is significantly larger than every other entry. Other important fields that dictate house size like number of bedrooms and bathrooms have clear correlations with house_size, those two attributes having a correlation of 0.45 and 0.62 respectively, so we can make similar conclusions about distribution from house_size for those fields as well.

Are there any data type issues (e.g. words in fields that were supposed to be numeric)? Where are these coming from? (E.g. a bug in your scraper? User input?) How will you fix them?
Yes, there was a data type issue with the zipcode column. Initially, zip codes were stored as integers, which led to the loss of leading zeros (e.g., 01001 was incorrectly displayed as 1001). This issue originated from the original realtor dataset, where zipcodes were incorrectly treated as numeric values instead of strings. Since ZIP codes are categorical and not meant for mathematical operations, they should always be stored as strings to maintain their correct format. To fix this issue, we converted the ZIP codes to strings and ensured they were consistently formatted as five-digit codes by prepending zeros where necessary.

Do you need to throw any data away? What data? Why? Any reason this might affect the analyses you are able to run or the conclusions you are able to draw?
We removed rows with missing values to ensure data quality and help reduce the sample size. Since we are tracking the actual sold solution price, we filtered the data by converting the prev_sold_date to a datetime and only keeping records with dates on or before a cutoff (2025-03-14) to remove houses that are still on the market.

Challenges/Observations and Next Steps
Summarize any challenges or observations you have made since collecting your data. Then, discuss your next steps and how your data collection has impacted the type of analysis you will perform. (approximately 3-5 sentences)
We initially attempted to scrape data directly, but the process proved too complex due to the need for IP proxies and dealing with dynamic content. We then resorted to using a Kaggle dataset; however, it was rejected by our TA because its authenticity (real versus synthetic) could not be confirmed. Ultimately, we found a real dataset that meets the project criteria, but it requires extensive cleaning and preprocessing. Moving forward,  we may explore relationships between prices and factors like house size, tax rates, and income levels to determine key drivers of price variation. The presence of categorical variables such as city and state suggests that location-based trends might also be significant, and we may use the chi-square test to analyze association between categorical variables. The structure of the dataset will influence whether we pursue regression modeling, t-test, etc. to derive insights.
