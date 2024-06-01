# Scrubbing data

After I'd obtained the data I needed for my analysis, it was time to scrub the data. Let me take you through what that involved in this video. First, I checked for duplicate values in my data. In my case, that was pretty straightforward, I could just check the countries listed in the country row of my data set and the years listed in the year rows to make sure there were no duplicates. I didn't expect any duplicate values because I downloaded this data straight from official databases that had been vetted by many researchers already. And indeed, I did not find any duplicates to remove. But I still had to remove some data, you might remember that I only wanted to focus on data from 2010 until 2021. But when I downloaded the data set, it came with more data than I needed. So I removed the columns with the years of data that I did not need. I did that for all the data sets I had downloaded. Next, I had to format records, this was pretty straightforward for my data as well, because after downloading the data, it came through nicely formatted already. I just double checked that the format was good. I made sure, for instance, that the numbers were indeed formatted as numbers in the spreadsheet, but it was all good, so I did not have anything to do here. Next, I checked for missing values, and as you might note, there were some missing values in my data set. First, I went back into the source data in Eurostat to double check. these values were indeed missing in the database, and that this was not some sort of glitch from downloading the data. But indeed, these data points were not available there can be different reasons for that, like a country not having reported the data, but there was really no way for me to replace them with actual data. In the data set, the missing data points were reflected by a colon or two vertical dots. That is okay, but I like to use letters instead, just to make sure there is no confusion when I start to use formulas later on. So I replaced these missing value indicators with NA. I'm showing you a piece of one of my data spreadsheets here, but I did the same for all of the data sets I used. Note that the data for 2021 had quite a few missing values. That is because it takes some countries longer to report their data than others, and the data for these countries was not available yet when I did my analysis. So I decided to take out all the data for 2021 from my analysis. As a final step in cleaning my data, I had to check for wrong values. Given that my data came from a trustworthy source, I didn't expect any wrong values, but I checked anyway to make sure and could not find anything. There was, however, one issue with my data I was collecting information about childcare, and it was quite obvious in my data that the year 2020 was a bit of an outlier. I had expected this to happen, 2020 was the year of the COVID-19 pandemic, and childcare options were often not available, even in countries where childcare was usually very accessible. I thought that this would affect my analysis, and because I had data for many years prior to 2020, I decided not to include the 2020 data at all. They weren't wrong, they were reported correctly, but 2020 was such an outlier when it came to childcare that I decided not to use the data in my analysis. So I took out all the data related to that year. Now my data sets are ready for further exploration, I'll focus on that in the next video.