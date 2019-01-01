[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

**Exercise 1**  
The distribution of income is famously skewed to the right. In this exercise, **_we’ll measure how strong that skew is._**

The Current Population Survey (CPS) is a joint effort of the Bureau of Labor Statistics and the Census Bureau to study income and related variables. Data collected in 2013 is available from http://www.census.gov/hhes/www/cpstables/032013/hhinc/toc.htm. I downloaded hinc06.xls, which is an Excel spreadsheet with information about household income, and converted it to hinc06.csv, a CSV file you will find in the repository for this book. You will also find hinc2.py, which reads this file and transforms the data.

The dataset is in the form of a series of income ranges and the number of respondents who fell in each range. The lowest range includes respondents who reported annual household income “Under $5000.” The highest range includes respondents who made “$250,000 or more.”

To estimate mean and other statistics from these data, we have to make some assumptions about the lower and upper bounds, and how the values are distributed in each range. hinc2.py provides InterpolateSample, which shows one way to model this data. It takes a DataFrame with a column, income, that contains the upper bound of each range, and freq, which contains the number of respondents in each frame.

It also takes log_upper, which is an assumed upper bound on the highest range, expressed in log10 dollars. The default value, log_upper=6.0 represents the assumption that the largest income among the respondents is 106, or one million dollars.

_InterpolateSample_ generates a pseudo-sample; that is, a sample of household incomes that yields the same number of respondents in each range as the actual data. It assumes that incomes in each range are equally spaced on a log10 scale.

```python
def InterpolateSample(df, log_upper=6.0):
    """Makes a sample of log10 household income.

    Assumes that log10 income is uniform in each range.

    df: DataFrame with columns income and freq
    log_upper: log10 of the assumed upper bound for the highest range

    returns: NumPy array of log10 household income
    """
    # compute the log10 of the upper bound for each range
    df['log_upper'] = np.log10(df.income)

    # get the lower bounds by shifting the upper bound and filling in
    # the first element
    df['log_lower'] = df.log_upper.shift(1)
    df.loc[0, 'log_lower'] = 3.0

    # plug in a value for the unknown upper bound of the highest range
    df.loc[41, 'log_upper'] = log_upper

    # use the freq column to generate the right number of values in
    # each range
    arrays = []
    for _, row in df.iterrows():
        vals = np.linspace(row.log_lower, row.log_upper, row.freq)
        arrays.append(vals)

    # collect the arrays into a single sample
    log_sample = np.concatenate(arrays)

    return log_sample
  ```

Compute the median, mean, skewness and Pearson’s skewness of the resulting sample. What fraction of households reports a taxable income below the mean? How do the results depend on the assumed upper bound?

```python
import hinc
income_df = hinc.ReadData()

uppers=[5, 6, 7]
income_df = hinc.ReadData()

# checking the effects of assumed upper bounds
for each in uppers:    
    log_sample = InterpolateSample(income_df, log_upper= each)
    sample = np.power(10, log_sample)
    print('Upper bound: 10^%s' %each)
    print('Mean: %s, Median: %s' %(Mean(sample), Median(sample)) )
    print('Skewness: %s, PearsonMedianSkewness: %s' %(Skewness(sample), PearsonMedianSkewness(sample)) )

    below_mean = sample[sample < Mean(sample)]
    fractionBelowMean = len(below_mean)/len(sample)
    print('Fraction below the mean: %s\n' %fractionBelowMean)

# OUTPUT
#Upper bound: 10^5
#Mean: 65308.999905353514, Median: 51226.45447894046
#Skewness: 1.1795507798229026, PearsonMedianSkewness: 0.8101024492937389
#Fraction below the mean: 0.6034558787502654

#Upper bound: 10^6
#Mean: 74278.70753118733, Median: 51226.45447894046
#Skewness: 4.949920244429583, PearsonMedianSkewness: 0.7361258019141782
#Fraction below the mean: 0.660005879566872

#Upper bound: 10^7
#Mean: 124267.39722164685, Median: 51226.45447894046
#Skewness: 11.603690267537793, PearsonMedianSkewness: 0.39156450927742087
#Fraction below the mean: 0.8565630665207663
```
> When the **upper bound** is _increased_, **sample skewness** is _increased_, and the fraction of household reporting below the mean also _increases_
