Previously, we discussed summary statistics and how they're a useful tool in data analytics. Although they give us a good starting point, we'll need to delve a bit deeper to truly understand our data. And that's where examining data distributions comes in.

### What is Data Distribution?

Basically, it's a way of showing how our data is spread across different values. Each dataset has its own unique look or distribution—it's kind of like a data fingerprint.

#### Categorical Data

Let's examine some categorical data. We can create a bar chart where the height of each bar corresponds to the frequency. Think of frequency as the number of times a particular value shows up for roll-call in our dataset. For example, if "TV" appears only twice while "Newsletter" appears four times, the "Newsletter" bar will be twice as high as the "TV" bar. Sorting the bars from highest to lowest frequency makes it even easier to spot the top categories.

#### Numerical Data

What about numerical data? By using a technique known as binning, we can treat numerical data as categorical data. These numbers represent the values of a dataset. All we need to do is group values together into what we call bins. Think of bins like little buckets, each holding data that falls within a range of values.

For instance, if we use a range of 10, one bin will hold any value from 0-10, another bin will hold values from 11-20, and a last bin will hold values from 21-30. Turning this new "binned" data into a bar chart gives us a histogram. In a histogram, the height of each bar tells us how many data points fell into each bucket or bin.

### Understanding Distributions

One of the most common or "normal" distributions is aptly named the "normal distribution." Picture the heights of a group of people. If you make a histogram of everyone's height, you'll see a curve that looks like a bell. This bell curve is symmetrical with the mean, median, and mode in the middle, and the spread of the data is determined by its standard deviation. Most people's heights are close to the average height, and very few people have heights far from the average. The low-frequency values on the left and right edges of the distribution are known as tails.

However, data fingerprints rarely fit perfectly into specific shapes. Here are a few other types of distributions:

1. **Bimodal Distribution**: This shape resembles a camel with two humps, indicating two distinct peaks in the data.
2. **Log-Normal Distribution**: This distribution is skewed, with the peak towards one side. This asymmetry indicates that most data points are on one end of the scale with a long tail extending to the other end.
3. **Exponential Distribution**: This is great for modeling random events over time, such as the time between customers arriving at a service counter. The peak is around zero, with a rapid decline and a long tail.
4. **Uniform Distribution**: Here, every bin has the same frequency, as you might see if you made a histogram of the results of rolling a die.

### Why Look at Data Distributions?

Data distributions serve as guides in the vast world of data. By examining the edges of the chart, you can quickly get an idea of your minimum and maximum values. You can identify the mode by looking for the bin with the highest frequency. If your histogram is tall and skinny, your data has a low standard deviation. If it's wide and flat, your data has a high standard deviation.

### Conclusion

Histograms are incredibly powerful tools that reveal stories hidden in our data—stories that mere numbers alone cannot tell. They help us visualize and understand these stories, guiding us to better decisions. Later, we will explore how to use these insights from data distributions when modeling and interpreting data. For now, practice creating and interpreting histograms to get a better grasp of the unique fingerprints of your datasets.