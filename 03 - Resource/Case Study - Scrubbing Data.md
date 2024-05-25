**Objective:**
- Select the 10 products for the subscription service to help Inu and Neko achieve 500 subscribers by the end of the year.

**Steps Taken:**

1. **Remove Duplicate Records:**
   - Kiara checked for duplicate entries but found none, as expected.

2. **Check Data Formatting:**
   - Kiara noticed irregularities in ZIP code formatting.
   - Decided to standardize ZIP codes to the shorter format for consistency.

3. **Handle Missing Values:**
   - Found missing entries for phone numbers, sales totals, and customer IDs.
   - Removed the phone number column as it was optional and not essential for analysis.
   - Filled in missing sales totals as they are calculated values.
   - Discarded entries with no customer IDs as they were deemed less valuable for analysis.

4. **Check for Inaccurate Information:**
   - Identified entries with negative sales totals as product returns.
   - Kept these entries to avoid bias in the analysis.
   - Removed entries with extremely high or negative product prices as they were clearly errors.

**Conclusion:**
- Kiara successfully scrubbed the dataset, addressing duplicate records, inconsistent formatting, missing values, and inaccurate information.
- The dataset is now clean and ready for the next step in the analysis process, exploring the data to select the subscription products.