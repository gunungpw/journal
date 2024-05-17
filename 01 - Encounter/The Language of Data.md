### Introduction to Data Literacy

Together, we've laid a solid foundation by navigating through the basics of data and the OSEMN framework. Today, we're ready to learn what I like to call the **language of data**, a skill essential for any aspiring data analyst. Think of data literacy as learning a new language like French or Spanish. The more fluent you become, the more proficient you'll be in using it.

### Asking Questions About Your Data

#### Data Sources and Files
Start by asking: **How many different data sources do I have?**
- **Multiple Files:** Determine if each data source comprises multiple files that need to be combined. For instance, your sales data might be a series of monthly reports.
- **File Sizes:** Note the size of each file—are they a few kilobytes or many gigabytes? This helps gauge the volume of data.

#### Data Dimensions
Once you understand the amount of data, familiarize yourself with each dataset:
- **Rows and Columns:** Count the number of rows and columns to map out the data's structure.

#### Data Types and Characteristics
Next, figure out the types of data in each column:
- **Data Types:** Identify numerical data, text data, boolean data (true/false), and date/time data.
- **Numerical vs. Categorical:** Distinguish between numerical (quantitative) and categorical (qualitative) data. Categorical data includes distinct groups like ice cream flavors or a rating scale from 1-5, which can sometimes be treated as numerical data.

### Using Summary Statistics

Given the large size of datasets, it's impractical to examine each data point. Instead, data analysts use **summary statistics** to get a quick snapshot:
- **Categorical Data:** Determine the number of different categories. For example, in a "Marketing Channel" column, you might have categories like Email, TV, and Social Media. Count the frequency of each category.
- **Numerical Data:** Find key statistics such as:
  - **Minimum and Maximum Values:** The smallest and largest values.
  - **Median:** The middle value when data is ordered.
  - **Mode:** The most frequently appearing value.
  - **Mean:** The average value.
  - **Standard Deviation:** Measures how much values differ from the mean.

### Exploring Raw Data

While summary statistics provide valuable insights, sometimes a simple review of raw data can be insightful:
- **Head and Tail:** Look at the first few rows (head) and the last few rows (tail) of the dataset.
- **Random Sampling:** Examine a random sample of data points to gain additional insights.

### Practical Example: Marketing Channels
Suppose you have a dataset with a column labeled "Marketing Channel." Here's how you might apply these concepts:
- **Categories:** Identify that there are three categories—Email, TV, and Social Media.
- **Frequencies:** Count that there are 3 Email records, 1 Social Media record, and 4 TV records.
- **Numerical Insights:** If you had numerical data on spending for each channel, you could calculate the mean, median, mode, minimum, maximum, and standard deviation to understand spending patterns.

### Conclusion

In this lesson, we've discussed understanding the size and structure of your dataset, the unique properties of data fields, and some basic yet useful summary statistics. Understanding the language of data is not just a theoretical exercise—it's a crucial tool that helps you uncover insights in your data analytics work. By mastering this language, you'll be better equipped to make sense of your data and extract meaningful insights.