# Vehicle Manufacturer Statistical Analysis with R

This is a class assignment for the Statistical Models course at EdgeHub, taught by M.Sc. Axel Torres. The dataset is `data/vehicles.csv`, a sample of 50 vehicles with the kind of specs a manufacturer might put in an ad: fuel performance, horsepower, weight, acceleration, model year, and country of origin.

The assignment asks for a full walkthrough of descriptive statistics and inference on that data:

1. Central tendency (mean, median, mode) for the main variables.
2. Measures of dispersion (standard deviation, interquartile range) for the variables where it makes sense to compute them.
3. Boxplots for those same variables.
4. A goodness-of-fit test on the country-of-origin categories.
5. An interpretation of what all of this actually means for a company selling these vehicles.

Everything lives in `notebook.ipynb`, written in R. The columns keep their original Spanish names from the professor's dataset (`Rendimiento_mpg`, `Caballos_de_Fuerza`, `Peso`, `Aceleracion`, `Año`, `Origen`); a translation table is in the notebook itself, and the original variable dictionary from the assignment is in `figures/variables.png`.

## A couple of things worth knowing before reading the notebook

**`Origen` is categorical, not numeric.** It stores country of origin as codes (1 = National, 2 = Foreign, 3 = Undetermined), so a mean or median of it doesn't mean anything statistically. Those two are still computed in the notebook because the assignment explicitly asks for them, but they're flagged as meaningless in the notebook's own observations. The mode is the only central tendency measure that actually applies to this variable.

**R has no built-in `mode()` function for this.** The base R `mode()` tells you the storage type of an object (numeric, character, and so on), not the statistical mode. So the notebook defines its own `mode_col()` function using `unique()`, `match()`, and `tabulate()`. If that combination looks unfamiliar, `MODE_ALGO.md` walks through why it works, step by step, with a worked example.

## Running it

You'll need R with the `dplyr`, `IRdisplay`, and `skimr` packages, plus a Jupyter setup with the R kernel (IRkernel) so `notebook.ipynb` can run. The first cell installs the packages if they're missing.
