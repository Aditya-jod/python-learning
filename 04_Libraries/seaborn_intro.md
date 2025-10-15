# Seaborn — Introduction and end-to-end learning

Seaborn is a high-level statistical plotting library built on top of Matplotlib. It provides a concise API for common statistical visualizations, sensible default styles, and easy integration with pandas DataFrames. This guide covers installation, core plot types, styling, working with datasets, and end-to-end examples.

## Quick setup

Install Seaborn (and pandas/matplotlib if needed):

```powershell
python -m pip install --upgrade pip; python -m pip install seaborn pandas matplotlib
```

Import convention:

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
```

## Dataset utilities

Seaborn ships example datasets accessible via `sns.load_dataset('name')`. Useful ones: `tips`, `iris`, `penguins`, `titanic`, `flights`.

```python
tips = sns.load_dataset('tips')
tips.head()
```

You can pass any pandas DataFrame to Seaborn plotting functions.

## Styles and context

Seaborn provides themes and contexts to control aesthetics:

```python
sns.set_theme(style='whitegrid', context='notebook')  # global
sns.set_style('darkgrid')                            # alternative
sns.set_context('talk', font_scale=1.1)              # larger fonts for presentations
```

Color palettes:

```python
sns.color_palette('deep')
sns.set_palette('pastel')
sns.color_palette('rocket', as_cmap=True)
```

## High-level plotting functions

Seaborn favors functions that work directly with DataFrame columns and semantic mappings (hue, size, style).

- Relational plots (scatter / line)
  - sns.relplot (figure-level), sns.scatterplot, sns.lineplot (axes-level)
```python
sns.relplot(data=tips, x='total_bill', y='tip', hue='smoker', height=5)
```

- Categorical plots
  - sns.catplot (figure-level), sns.boxplot, sns.violinplot, sns.stripplot, sns.barplot, sns.pointplot
```python
sns.boxplot(data=tips, x='day', y='total_bill', hue='sex')
```

- Distribution plots
  - sns.histplot, sns.kdeplot, sns.displot (figure-level)
```python
sns.histplot(data=tips, x='total_bill', kde=True, bins=30)
```

- Regression / statistical relationships
  - sns.lmplot (figure-level), sns.regplot (axes-level)
```python
sns.lmplot(data=tips, x='total_bill', y='tip', hue='smoker', scatter_kws={'alpha':0.6})
```

- Matrix / heatmap
  - sns.heatmap for correlation matrices or pivot tables
```python
corr = tips.corr()
sns.heatmap(corr, annot=True, fmt='.2f', cmap='coolwarm')
```

- Pairwise relationships
  - sns.pairplot for quick EDA across multiple variables
```python
sns.pairplot(sns.load_dataset('iris'), hue='species', corner=True)
```

## Figure-level vs axes-level

- Figure-level: sns.relplot, sns.catplot, sns.displot, sns.pairplot, sns.lmplot — create their own FacetGrid and manage faceting.
- Axes-level: sns.scatterplot, sns.boxplot, sns.histplot, sns.heatmap — draw on an existing Matplotlib Axes (useful inside subplots).

## Faceting

Faceting creates multiple subplots conditioned on column values:

```python
sns.relplot(data=tips, x='total_bill', y='tip', col='time', row='smoker', hue='sex')
```

## Customization and combining with Matplotlib

You can fine-tune plots using Matplotlib after Seaborn draws them:

```python
ax = sns.scatterplot(data=tips, x='total_bill', y='tip')
ax.set_title('Tips vs Bill')
ax.set_xlabel('Total bill ($)')
plt.tight_layout()
plt.savefig('tips_scatter.png', dpi=150)
```

For complex layouts, create Matplotlib subplots and pass axes to axes-level Seaborn functions.

## Example: end-to-end script (save as seaborn_example.py)

```python
# filepath: d:\Data Science Projects\python-learning\04_Libraries\seaborn_example.py
import seaborn as sns
import matplotlib.pyplot as plt
sns.set_theme(style='whitegrid', context='notebook')

tips = sns.load_dataset('tips')
fig, ax = plt.subplots(figsize=(8,5))
sns.scatterplot(data=tips, x='total_bill', y='tip', hue='time', size='size', alpha=0.7, ax=ax)
ax.set_title('Tips vs Total Bill')
plt.tight_layout()
fig.savefig('tips_example.png', dpi=150)
plt.show()
```

Run it (PowerShell):

```powershell
python .\04_Libraries\seaborn_example.py
```

Or in a Jupyter notebook use `%matplotlib inline` and rerun the cells.

## Performance and tips

- Use figure-level functions for quick faceted plots; axes-level for precise control.
- For large datasets, sample or use alpha to manage overplotting.
- Combine with pandas pivot_table to create tidy inputs for heatmaps.
- When saving figures for publication, set dpi and use vector formats (PDF/SVG) when appropriate.

## Common pitfalls

- Mixing figure-level and axes-level calls incorrectly can create unexpected figures.
- Some Seaborn styles require Matplotlib/Seaborn versions — update packages if behavior differs.
- Beware of categorical ordering; use `order=` or convert to Categorical with desired categories.

## References

- Seaborn docs: https://seaborn.pydata.org/
- Examples & gallery: https://seaborn.pydata.org/examples/index.html
