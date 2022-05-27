# Data Science & AI
Imports: 
```
import numpy as np                              
import scipy.stats as stats   

import pandas as pd                                
from pandas.api.types import CategoricalDtype

import matplotlib.pyplot as plt                     
from statsmodels.graphics.mosaicplot import mosaic  
import seaborn as sns                               
import altair as alt
```
## Hoofdstuk 1
- read csv: `dataset = pd.read_csv("path", delimiter = "teken om te splitsen")`
- basic operation on dataset:
  - `.info()` = general information
  - `len(dataset)` = aantal rijen
  - `len(dataset.columns)` = aantal kolommen
  - `dataset.shape` = rijen en kolommen
  - `dataset.dtypes (.value_counts())` = datatype elke kolom | tel kolommen per datatype
  - `dataset.describe()` = overzicht count, mean, std, min, kwartielen, max
- index instellen: `dataset.set_index(['KolomNaam'])`
- kwalitatieve variabelen instellen: `dataset.KolomNaam = dataset.KolomNaam.astype('category')`
- unieke items in kolom: `dataset.KolomNaam.unique()`
- ordinale ordening instellen: 
  - `ordening = CategoricalDtype(categories=['x1', 'x2', 'x3'], ordered=True)`
  - `dataset.KolomNaam = dataset.KolomNaam.astype(ordening)`
- rijen uitprinten: `dataset.iloc[value]`
- voorwaarden opleggen (vb.): `dataset[dataset['KolomNaam'] < waarde][['KolomNaam', 'KolomNaam']]`
- query (vb.): `dataset.query("(KolomNaam ==  'waarde') and (KolomNaam < waarde)")`
- kolom verwijderen: `dataset = dataset.drop("KolomNaam", axis="columns")`
- elke rij verwijderen met missing waarden: `datasetClean = dataset.dropna()`
- enkel rijen verwijderen die volledig uit missing waarden bestaan: `datasetClean = dataset.dropna(how="all")`
- gemiddelde: `dataset['KolomNaam'].mean()`
- lege waarden opvullen: `dataset = dataset.fillna(value={'KolomNaam': waarde})`
- nieuwe kolom toevoegen: `dataset['NieuweKolomNaam'] = iets`
- kolom toevoegen volgens functie of dictionary = `dataset['NieuweKolomNaam'] = dataset['KolomNaam'].map(dict/function)`

## Hoofdstuk 2
- voorgemaakte datasets inladen van Seaborn: `dataset = sns.load_dataset('naam')`
- modus: `dataset.mode()`
- standaardafwijking: `dataset['KolomNaam'].std()`
- variantie:`dataset['KolomNaam'].var()`
- skewness: `dataset['KolomNaam'].skew()`
- kurtosis: `dataset['KolomNaam'].kurtosis()`
- minimum: `dataset['KolomNaam'].min()`
- maximum: `dataset['KolomNaam'].max()`
- mediaan: `dataset['KolomNaam'].median()`
- range: `dataset['KolomNaam'].max() - dataset['KolomNaam'].min()`
- kwartielen:
  - `kwartielen = [0.0, 0.25, 0.5, 0.75, 1.0]`
  - `dataset['KolomNaam'].quantile(percentiles)`
  - `dataset['KolomNaam']['25% of 75']` 
- inter kwartiel afstand: `dataset['KolomNaam'].quantile(.75) - dataset['KolomNaam'].quantile(.25)`

- barchart: `sns.catplot(data = dataset, kind = "count", x = "KolomNaam", aspect = breedte)`
- boxplot: `sns.boxplot(data = dataset, x = "KolomNaam")`
- violinplot: `sns.violinplot(data = dataset, x = "KolomNaam")`
- probability density graph: `sns.kdeplot(x = dataset["KolomNaam"]);`
- histogram + prob dens: `sns.displot(x = dataset['KolomNaam'], kde=True);`
- barchart voor kwantitatieve variabelen: `sns.countplot(data = dataset, x = 'KolomNaam', hue = 'KolomNaam')`
- scatter diagram: 
  - `graph = sns.FacetGrid(data = dataset, col="KolomNaam", hue="KolomNaam")`
  - `graph.map(sns,kdeplot, "KolomNaam"`
  - `grapgh.add_legend()`

## Hoofdstuk 3
- plot probability density function: `plt.plot(dataset, stats.norm.pdf(dataset, 0, 1)`
  - 0 & 1 zijn default maar meestal gebruikt men m en s met m = gemiddelde en s = standaardafwijking
- data array met waarden creeren: `naam = np.linespace(startwaarde, eindwaarde, num=aantal)`
  - hier wordt voor start/eindwaarde vaak x standaard deviaties gebruikt dus (m - x * s) & (m + x * s)
- data array die een normaalverdeling heeft: `naam = np.random.normal(m, s, size=n)`
- plot histogram: `sns.histplot(dataset)`
- plot density histogram: `sns.histplot(dataset, stat = "density)`

Z-test
- left tail probability: `stats.norm.cdf(x, df=d)`
- right tail probability: `stats.norm.sf(x, df=d)`
- probability density op x: `stats.norm.pdf(x, df=d)`
- p% observations verwacht lager dan resultaat: `stats.norm.isf(1 - p, df=d)`  
- z score: `stats.norm.isf(alpha / 2)`
- grens links (lower): `m - z * s / np.sqrt(n)`
- grens rechts (higher): `m + z * s / np.sqrt(n)`


T-test
- left tail probability: `stats.t.cdf(x, m, s)`
- right tail probability: `stats.t.sf(x, m, s)`
- probability density op x: `stats.t.pdf(x, m, s)`
- p% observations verwacht lager dan resultaat: `stats.t.isf(1 - p, m, s)`
- t-score: `stats.t.isf(alpha/2, df = n - 1)`
- grens links (lower): `m - t * s / np.sqrt(n)`
- grens rechts (higher): `m + t * s / np.sqrt(n)`


- Left Tail probability plot
  ```
  # X-values
  dist_x = np.linspace(m - standaardafwijking * s, m + standaardafwijking * s, num=aantal waarden)
  
  # Y-values for drawing the Gauss curve
  dist_y = stats.norm.pdf(dist_x, m, s)
  
  # Plot the Gauss-curve
  plt.plot(dist_x, dist_y)
  
  # Fill the area left of x
  plt.fill_between(dist_x, 0, dist_y, where=dist_x <= x, color='lightblue')
  
  # Show the mean with an orange line
  plt.axvline(m, color="orange", lw=2)
  
  # Show x with a green line
  plt.axvline(x, color="green")
  ```
- Right Tail z-test
  ```
  # 1. Formulate hypotheses
  
  # 2. Properties of the sample:
  n = 30      # sample size
  sm = 3.483  # sample mean
  s = 0.55    # population standard deviation (assumed to be known)
  a = 0.05    # significance level (chosen by the researcher)
  m0 = 3.3    # hypothetical population mean (H0)
  
  # 3. Determine value of the test statistic, x (met streep op)
  
  # 4. Determine the p-value and reject H0 if p < alpha
  p = stats.norm.sf(sm, loc=m0, scale=s/np.sqrt(n))
  print("p-value: %.5f" % p)
  if(p < a):
    print("p < a: reject H0")
  else:
    print("p > a: do not reject H0")
    
  # g-waarde
  g = m0 + stats.norm.isf(a) * s / np.sqrt(n)
  print("Critical value g ≃ %.3f" % g)
  if (sm < g):
    print("sample mean = %.3f < g = %.3f: do not reject H0" % (sm, g))
  else:
    print("sample mean = %.3f > g = %.3f: reject H0" % (sm, g))
    
  # plot
  # X-values
  dist_x = np.linspace(m0 - 4 * s/np.sqrt(n), m0 + 4 * s/np.sqrt(n), num=201)

  # Y-values for the Gauss curve
  dist_y = stats.norm.pdf(dist_x, m0, s/np.sqrt(n))
  fig, dplot = plt.subplots(1, 1)
  
  # Plot the Gauss-curve
  dplot.plot(dist_x, dist_y)
  
  # Show the hypothetical population mean with an orange line
  dplot.axvline(m0, color="orange", lw=2)
  
  # Show the sample mean with a red line
  dplot.axvline(sm, color="red")
  
  # Fill the acceptance area in light blue
  dplot.fill_between(dist_x, 0, dist_y, where=dist_x <= g, color='lightblue')
  ```
- Left Tail z-test
  ```
  # 1. Formulate hypotheses
  
  # 2. Properties of the sample:
  n = 30      # sample size
  sm = 3.483  # sample mean
  s = 0.55    # population standard deviation (assumed to be known)
  a = 0.05    # significance level (chosen by the researcher)
  m0 = 3.3    # hypothetical population mean (H0)
  
  # 3. Determine value of the test statistic, x (met streep op)
  
  # 4. Determine the p-value and reject H0 if p < alpha
  p = stats.norm.cdf(sm, loc=m0, scale=s/np.sqrt(n))
  print("p-value: %.5f" % p)
  if(p < a):
    print("p < a: reject H0")
  else:
    print("p > a: do not reject H0")
    
  # g-waarde
  g = m0 + stats.norm.isf(a) * s / np.sqrt(n)
  print("Critical value g ≃ %.3f" % g)
  if (sm < g):
    print("sample mean = %.3f < g = %.3f: do not reject H0" % (sm, g))
  else:
    print("sample mean = %.3f > g = %.3f: reject H0" % (sm, g))
    
  # plot
  # X-values
  dist_x = np.linspace(m0 - 4 * s/np.sqrt(n), m0 + 4 * s/np.sqrt(n), num=201)

  # Y-values for the Gauss curve
  dist_y = stats.norm.pdf(dist_x, m0, s/np.sqrt(n))
  fig, dplot = plt.subplots(1, 1)
  
  # Plot the Gauss-curve
  dplot.plot(dist_x, dist_y)
  
  # Show the hypothetical population mean with an orange line
  dplot.axvline(m0, color="orange", lw=2)
  
  # Show the sample mean with a red line
  dplot.axvline(sm, color="red")
  
  # Fill the acceptance area in light blue
  dplot.fill_between(dist_x, 0, dist_y, where=dist_x <= g, color='lightblue')
  ```
- Two-tailed z-test
  ```
  # 1. Formulate hypotheses
  
  # 2. Properties of the sample:
  n = 30      # sample size
  sm = 3.483  # sample mean
  s = 0.55    # population standard deviation (assumed to be known)
  a = 0.05    # significance level (chosen by the researcher)
  m0 = 3.3    # hypothetical population mean (H0)
  
  # 3. Determine value of the test statistic, x (met streep op)
  
  # 4. Determine the p-value and reject H0 if p < alpha /2
  p = stats.norm.sf(sm, loc=m0, scale=s/np.sqrt(n))
  print("p-value: %.5f" % p)
  if(p < a/2):
    print("p < a/2: reject H0")
  else:
    print("p > a/2: do not reject H0")
    
  # g-waarde (nu hebben we er 2)
  g1 = m0 - stats.norm.isf(a/2) * s / np.sqrt(n)
  g2 = m0 + stats.norm.isf(a/2) * s / np.sqrt(n)

  print("Acceptance region [g1, g2] ≃ [%.3f, %.3f]" % (g1,g2))
  if (g1 < sm and sm < g2):
    print("Sample mean = %.3f is inside acceptance region: do not reject H0" % sm)
  else:
    print("Sample mean = %.3f is outside acceptance region: reject H0" % sm)
    
  # plot
  # X-values
  dist_x = np.linspace(m0 - 4 * s/np.sqrt(n), m0 + 4 * s/np.sqrt(n), num=201)
  
  # Y-values
  dist_y = stats.norm.pdf(dist_x, loc=m0, scale=s/np.sqrt(n))
  fig, dplot = plt.subplots(1, 1)
  
  # Plot
  dplot.plot(dist_x, dist_y)
  
  # Hypothetical population mean in orange
  dplot.axvline(m0, color="orange", lw=2)
  
  # Sample mean in red
  dplot.axvline(sm, color="red")
  acc_x = np.linspace(g1, g2, num=101)
  acc_y = stats.norm.pdf(acc_x, loc=m0, scale=s/np.sqrt(n))
  
  # Fill the acceptance region in light blue
  dplot.fill_between(acc_x, 0, acc_y, color='lightblue')
  ```
- Right-tailed t-test
  ```
  # 1. Formulate hypotheses
  
  # 2. Properties of the sample
  n = 20      # sample size
  sm = 3.483  # sample mean
  ss = 0.55   # sample(!) standard deviation
  a = 0.05    # significance level (chosen by the researcher)
  m0 = 3.3    # hypothetical population mean (H0)
  
  # 3. Determine value of the test statistic, x (met streep op)
  
  # 4. Determine the p-value and reject H0 if p < alpha
  p = p = stats.t.sf(sm, loc=m0, scale=s/np.sqrt(n), df=n-1)
  print("p-value: %.5f" % p)
  if(p < a):
    print("p < a: reject H0")
  else:
    print("p > a: do not reject H0")
    
  # g-waarde
  g = m0 + stats.t.isf(a, df=n-1) * s / np.sqrt(n)
  print("Critical value g ≃ %.3f" % g)
  if (sm < g):
    print("sample mean = %.3f < g = %.3f: do not reject H0" % (sm, g))
  else:
    print("sample mean = %.3f > g = %.3f: reject H0" % (sm, g))
  
  # plot
  # X-values
  dist_x = np.linspace(m0 - 4 * s/np.sqrt(n), m0 + 4 * s/np.sqrt(n), num=201)
  
  # Y-values
  dist_y = stats.t.pdf(dist_x, loc=m0, scale=s/np.sqrt(n), df=n-1)
  fig, dplot = plt.subplots(1, 1)
  
  # Plot
  dplot.plot(dist_x, dist_y)
  
  # Hypothetical population mean in orange
  dplot.axvline(m0, color="orange", lw=2)
  
  # Sample mean in red
  dplot.axvline(sm, color="red")
  
  # Fill the acceptance region in light blue
  dplot.fill_between(dist_x, 0, dist_y, where=dist_x <= g, color='lightblue')
  
  # Shortcut
  observations = [
  3, 2, 3, 1, 10, 4, 2, 7, 3, 0,
  3, 1, 2, 3,  4, 0, 3, 8, 3, 7]
  a = 0.05
  m0 = 3.3

  t_stat, p_val = stats.ttest_1samp(observations, m0)
  print("Sample mean        : %.3f" % np.mean(observations))
  print("t-score            : %.3f" % t_stat)
  print("p-value (2-tailed) : %.5f" % p_val)
  print("p-value (1-tailed) : %.5f" % (p_val/2))
  ```

## Hoofdstuk 4
- Chi-squared test
  ```
  observed = pd.crosstab(dataset.Kolom, dataset.Kolom)
  chi2, p, df, expected = stats.chi2_contingency(observed)

  print("Chi-squared       : %.4f" % chi2)
  print("Degrees of freedom: %d" % df)
  print("P-value           : %.4f" % p)
  
  # plot
  # x-values:
  x = np.linspace(0, 15, num=100)
  # probability density of the chi-squared distribution with 4 degrees of freedom
  y = stats.chi2.pdf(x, df=dof)
  # the number q for which the right tail probability is exactly 5%:
  q = stats.chi2.isf(alpha, df=4)  
  fig, tplot = plt.subplots(1, 1)
  tplot.plot(x, y)                     
  tplot.fill_between(x, y, where=x>=q, color='lightblue')
  tplot.axvline(q)                     
  tplot.axvline(chi2, color='orange')  
  ```
- Goodness of fit test
  ```
  alpha = waarde             # Significance level
  n = sum(observed)          # Sample size
  k = len(observed)          # Number of categories
  dof = k - 1                # Degrees of freedom
  expected = expected_p * n  # Expected absolute frequencies in the sample
  g = stats.chi2.isf(alpha, df=dof)  # Critical value

  # Goodness-of-fit-test in Python:
  chi2, p = stats.chisquare(f_obs=observed, f_exp=expected)

  print("Significance level  ⍺ = %.2f" % alpha)
  print("Sample size         n = %d" % n)
  print("k = %d; df = %d" % (k, dof))
  print("Chi-squared        χ² = %.4f" % chi2)
  print("Critical value      g = %.4f" % g)
  print("p-value             p = %.4f" % p)
  
  # plot
  # x-values:
  x = np.linspace(0, 15, num=100)
  # probability density of the chi-squared distribution with 4 degrees of freedom
  y = stats.chi2.pdf(x, df=dof)
  # the number q for which the right tail probability is exactly 5%:
  q = stats.chi2.isf(alpha, df=dof)

  fig, tplot = plt.subplots(1, 1)
  tplot.plot(x, y)
  tplot.fill_between(x, y, where=x>=q, color='lightblue')
  tplot.axvline(q)
  tplot.axvline(chi2, color='orange')
  ```
- margin totals CONTROLEREN: `pd.crosstab(dataset.Kolom, dataset.Kolom, margins=True)`
- margin totals BEREKENEN:
  ```
  row_sums = observed.sum(axis=1)
  col_sums = observed.sum()
  n = row_sums.sum()

  print(row_sums)
  print(col_sums)
  print(f'Number of observations: {n}')
  ```
- verwachte resultaten: `expected = np.outer(row_sums, col_sums) / n`
- X^2 test statistiek: `diffs = (expected - observed)**2 / expected`
- X^2: `chi_squared = diffs.values.sum()`
- Cramers V:
  ```
  dof = min(observed.shape) - 1
  cramers_v = np.sqrt(chi_squared / (dof * n))
  ```
- stacked bar chart: `observed.plot(kind='bar', stacked=True)`
- naam kolom wijzigen: `datset = datset.rename(columns={'Oude naam': 'Nieuwe naam'})`
- unieke waarden printen: `dataset.Kolom.unique()`

## Hoofdstuk 5
- T-test twee onafhankelijke samples: `stats.ttest_ind(a=dataset1, b=dataset2, alternative='less', equal_var=False)`
  - 'less' omdat we onderzoeken of a kleiner is dan b
- T-test twee afhankelijke samples: `stats.ttest_rel(a=dataset1, b=dataset2, alternative='less')`
  - 'less' omdat we onderzoeken of a kleiner is dan b
- Cohon's d:
  ```
  # function
  def cohen_d(a, b):
    na = len(a)
    nb = len(b)
    pooled_sd = np.sqrt( ((na-1) * a.std(ddof=1)**2 +
                          (nb-1) * b.std(ddof=1)**2) / (na + nb - 2) )
    return (b.mean() - a.mean()) / pooled_sd
    
  # use
  cohen_d(regular, additives)
  ```

## Hoofdstuk 6


## Hoofdstuk 7

