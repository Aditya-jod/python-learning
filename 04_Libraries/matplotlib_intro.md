# Matplotlib — Introduction and end-to-end learning

Matplotlib is the foundational plotting library in Python for creating static, animated, and interactive visualizations. This guide covers installation, basic plotting, the recommended object-oriented API, common plot types, styling, saving figures, and running examples end-to-end.

## Quick setup

Install Matplotlib (and optionally seaborn for nicer defaults):

```powershell
python -m pip install --upgrade pip; python -m pip install matplotlib seaborn
```

Import convention:

```python
import matplotlib.pyplot as plt
import numpy as np
```

If using Jupyter notebooks, enable inline display:

```python
%matplotlib inline           # simple static images in notebook
# or for interactive backends:
%matplotlib notebook
```

## Two APIs: Pyplot (stateful) vs Object-Oriented (recommended)

- pyplot: quick and simple (plt.plot, plt.show). Good for exploration.
- OO API: create Figure and Axes objects and call methods on them. Preferred for complex or repeatable plots.

OO example:

```python
fig, ax = plt.subplots()
ax.plot(x, y, label='line')
ax.set_title('Title')
ax.set_xlabel('x')
ax.set_ylabel('y')
ax.legend()
fig.savefig('out.png', dpi=150)
```

## Basic line plot

```python
import numpy as np, matplotlib.pyplot as plt
x = np.linspace(0, 10, 200)
y = np.sin(x)
fig, ax = plt.subplots(figsize=(6,3))
ax.plot(x, y, color='tab:blue', lw=2, label='sin(x)')
ax.axhline(0, color='k', linewidth=0.5)
ax.set_xlabel('x')
ax.set_ylabel('sin(x)')
ax.set_title('Sine wave')
ax.legend()
plt.show()
```

## Scatter, bar, and histogram

Scatter:

```python
rng = np.random.default_rng(0)
x = rng.normal(size=200)
y = x*0.5 + rng.normal(scale=0.8, size=200)
fig, ax = plt.subplots()
ax.scatter(x, y, c=x, cmap='viridis', alpha=0.7)
ax.set_title('Scatter plot')
```

Bar:

```python
categories = ['A','B','C']
values = [10, 24, 7]
fig, ax = plt.subplots()
ax.bar(categories, values, color=['#4C72B0','#DD8452','#55A868'])
ax.set_ylabel('Value')
```

Histogram:

```python
data = rng.normal(size=1000)
fig, ax = plt.subplots()
ax.hist(data, bins=30, color='gray', edgecolor='black')
ax.set_title('Histogram')
```

## Subplots and grids

```python
fig, axs = plt.subplots(2, 2, figsize=(8,6), constrained_layout=True)
axs[0,0].plot(x, np.sin(x))
axs[0,1].scatter(x, np.sin(x))
axs[1,0].hist(rng.normal(size=500))
axs[1,1].bar(categories, values)
```

Use constrained_layout=True or fig.tight_layout() to avoid overlap.

## Styling and colors

- Use color names ('red', 'blue'), hex ('#1f77b4'), or tab colors ('tab:blue').
- Line styles: '-', '--', '-.', ':'
- Markers: 'o', 's', '^'
- Colormaps: plt.cm.viridis, 'plasma', 'inferno'

Seaborn integrates well for improved defaults:

```python
import seaborn as sns
sns.set(style='whitegrid', context='notebook')
```

## Legends, annotations, and text

```python
ax.plot(x, y, label='sin')
ax.legend(loc='upper right')
ax.annotate('peak', xy=(1.57, 1), xytext=(2, 1.5),
            arrowprops=dict(arrowstyle='->', color='black'))
ax.text(0.1, 0.9, 'Sample text', transform=ax.transAxes)
```

## Axes scales and formatting

- Log scale: ax.set_yscale('log')
- Date axis: use matplotlib.dates for formatting
- Custom tick formatters and locators for fine control

## Saving figures

```python
fig.savefig('figure.png', dpi=150, bbox_inches='tight')  # PNG
fig.savefig('figure.pdf')                                # Vector PDF
```

Common formats: PNG, PDF, SVG, EPS.

## Interactive and animations

- For interactivity use interactive backends (Qt5Agg, TkAgg) or libraries like mplcursors.
- For animations use matplotlib.animation.FuncAnimation.

## Performance tips

- For large scatter plots, use rasterized=True or datashader for millions of points.
- Reuse Figure and Axes objects rather than creating many figures in loops.
- Save vector formats for publication; raster formats for screenshots.

## Example: end-to-end script (save as example_plot.py)

```python
# filepath: d:\Data Science Projects\python-learning\04_Libraries\example_plot.py
import numpy as np
import matplotlib.pyplot as plt
from numpy.random import default_rng

rng = default_rng(0)
x = np.linspace(0, 10, 300)
y1 = np.sin(x)
y2 = np.cos(x)

plt.style.use('seaborn-v0_8')  # optional; requires seaborn installed for full effect
fig, ax = plt.subplots(figsize=(8,4))
ax.plot(x, y1, label='sin', color='tab:blue')
ax.plot(x, y2, label='cos', color='tab:orange', linestyle='--')
ax.set_title('Sine and Cosine')
ax.set_xlabel('x')
ax.set_ylabel('y')
ax.legend()
ax.grid(True)
fig.savefig('sine_cosine.png', dpi=150)
plt.show()
```

Run it (PowerShell):

```powershell
python .\04_Libraries\example_plot.py
```

Or in notebook:

```python
%matplotlib inline
from IPython.display import Image
Image('04_Libraries/sine_cosine.png')
```

## Common pitfalls

- Forgetting plt.show() in scripts; in notebooks plots display automatically.
- Overplotting many points without alpha blending.
- Not using the OO API when creating multiple axes — leads to confusion about which axes plt functions act on.

## Next steps / learning path

- Learn seaborn for statistical plotting and nicer themes.
- Explore interactive plotting: Plotly, Bokeh, or Altair.
- Practice with real datasets: scatter matrix, pairplot, time-series plotting.
- Create a Jupyter notebook with multiple cells to experiment with styles, colormaps, and subplots.

## References

- Matplotlib docs: https://matplotlib.org/stable/contents.html
- Tutorials: official examples gallery on the Matplotlib website