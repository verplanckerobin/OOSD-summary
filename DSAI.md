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


## Hoofdstuk 4


## Hoofdstuk 5


## Hoofdstuk 6


## Hoofdstuk 7

