[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

> Cohen's D is used to quantify (or measure) the difference between two groups of data, to reveal whether the effect between the two groups is large enough and consistent enough to be really important

**Exercise 4**   *Using the variable totalwgt_lb, investigate whether first babies are lighter or heavier than others. Compute Cohen’s* d *to quantify the difference between the groups. How does it compare to the difference in pregnancy length?*

Code:
```python
def CohenEffectSize(group1, group2):
     """Computes Cohen's effect size for two groups
     group1: Series or DataFrame
     group2: Series or DataFrame
     returns: float if the arguments are Series;
          Series if the arguments are DataFrames
     """
     diff = group1.mean() - group2.mean()
      
    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)
    
    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / np.sqrt(pooled_var)
 
    return d
```

```python
# Import data
preg = nsfg.ReadFemPreg()
live = preg[preg.outcome == 1]
# get a subset of first and others
firsts = live[live.birthord == 1]
others = live[live.birthord != 1]

# Solution
CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb)

# The output is -0.08867292707260174
```
__conclusion:__
- _Cohen's d_ for baby weights (-0.089) is small, i.e., the difference in weight between first babies and others are not very substantial, or it's only observable under a very [careful study](http://staff.bath.ac.uk/pssiw/stats2/page2/page14/page14.html)
-  Compared to _Cohen's d_ for pregnancy length (0.029), the difference in weight_lb groups is less obvious, and the effect [decreases the mean](https://trendingsideways.com/the-cohens-d-formula)