# data_deliverable
# a complete data spec
Attribute Descriptions:
Price: float
Default value: n/a
Range: 600.0 - 39000000.0
Distribution Analysis: heavily depends on location 
Unique?: no
Use to detect duplicates?: no
Required?: yes
Will use in analysis?: Yes, price is an important indicator and is likely to be highly correlated to many other important fields like homeowner income, state tax, and house size.
Sensitive?: no


Bed: int
Default value: 1.0
Range: 1.0 - 19.0
Distribution Analysis: has a positive correlation with price, bath, and house_size
Unique?: no
Use to detect duplicates?: yes, we can combine this with bath, house_size, city, and state to create a good identifier for this entry
Required?: yes
Will use in analysis?: Yes, number of bedrooms is likely to be highly correlated with house_size, which itself can inform a number of useful trends 
Sensitive?: no


Bath: int
Default value: 1.0
Range: 1.0 - 16.0
Distribution Analysis: has a positive correlation with price, bed, house_size
Unique?: no
Use to detect duplicates?: yes, we can combine this with bed, house_size, city, and state to create a good identifier for this entry
Required?: yes
Will use in analysis?: Yes, number of bathrooms is likely to be highly correlated with house_size, which itself can inform a number of useful trends 
Sensitive?: no


Status: string
Default value: “For sale”
Range: {“for_sale”, “sold”}
Distribution Analysis: not correlated with anything else in our dataset
Unique?: no
Use to detect duplicates?: no
Required?: no
Will use in analysis?: no, not very related to the rest of the attributes and our hypotheses
Sensitive?: no


Zip_code: string 
Default value: n/a
Range: Must be one of the values in this list: https://postalpro.usps.com/ZIP_Locale_Detail
Distribution Analysis: based on geographic location, zip codes associated with larger cities will have more entries with the same zip code
Unique?: no
Use to detect duplicates?: yes, can use this as a metric of location
Required?: no
Will use in analysis?: no, while zip code is a useful way of finding useful financial information relating to a particular area, we have already found some useful financial information to be joined here, so zip code itself is not so useful
Sensitive?: no


House_size: float
Default value: 0.0
Range: 246.0 - 247421.0
Distribution Analysis: is likely to be positively correlated with price, bed, and bath
Unique?: no
Use to detect duplicates?: yes, house size is a good way of telling uniqueness of a house since it is unlikely too many houses have the exact same size
Required?: yes
Will use in analysis?: yes, house_size is likely to be connected to wealth of a region, which has strong implications for homeowner income, and possibly for taxation
Sensitive?: no


Effective tax rate: float
Default value: 0.0
Range: 0.27% - 2.23%
Distribution Analysis: we averaged based on state, so this has a 1-to-1 mapping with state
Unique?: no
Use to detect duplicates?: no, this is exactly the same as state, which itself is not unique to a house
Required?: yes
Will use in analysis?: yes, tax is a major element of what we are trying to test for
Sensitive?: no


2023_avg_income: float
Default value: 0.0
Range: 39952.0949609859 - 219892.6275283541
Distribution Analysis: only one value, all entries have the same value
Unique?: no
Use to detect duplicates?: no
Required?: yes
Will use in analysis?: yes, income of homeowners relating to the area they are living in is a major element that we want to test for
Sensitive?: no
