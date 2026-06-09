Overview
This R script performs standardization, correlation analysis, principal component analysis (PCA), and both static and interactive visualizations on morphometric data. Key features include:

Range normalization of all numeric variables to [0,1]

Spearman rank correlation analysis with significance filtering (p > 0.05 set to zero)

Principal component analysis (PCA) for dimensionality reduction

2D PCA biplots with optional grouping and 95% confidence ellipses

Interactive 3D scatter plot of the first three principal components with loading vectors (arrows)

Required Libraries
Install and load the following R packages before running the script:

r
install.packages(c("vegan", "factoextra", "plotly"))
vegan – provides decostand for range standardization

factoextra – provides fviz_pca_biplot for PCA visualization

plotly – provides interactive 3D plotting

Input Data Format
File name: data_morphometry.txt (tab‑separated, with header)

First column: group labels (e.g., sex, species, treatment). This column is stored as p_names and used for coloring in PCA biplots.

Remaining columns: numeric morphometric variables (each column represents one trait).

Execution Steps
Set locale (optional) – uncomment the Sys.setlocale line if Russian text encoding is needed.

Read data – load the tab‑separated file.

Separate labels and numeric data – store the first column as grouping factor, remove it from the data matrix.

Range normalization – apply min‑max scaling to each numeric column using decostand(..., method = "range").

Spearman correlation – compute correlation coefficients and p‑values for all variable pairs; set non‑significant correlations (p > 0.05) to zero.

PCA – run prcomp on the normalized data, display variance explained.

2D PCA biplots – generate three variants:

Simple biplot (no grouping)

Biplot with points colored by p_names

Biplot with colored points and 95% confidence ellipses

Interactive 3D plot – extract PC1, PC2, PC3 scores and variable loadings; create an interactive scatter plot (points colored by PC2 value) and add loading vectors as scaled arrows.

Outputs
Console output: summary of PCA variance explained.

Static plots (displayed in R graphics device):

Basic PCA biplot

Colored biplot (by group)

Colored biplot with 95% confidence ellipses

Interactive 3D plot (opens in browser / RStudio Viewer):

Sample scores shown as markers (color gradient from #FFE1A1 to #683531 based on PC2 values)

Loading vectors as thick lines (scaled by factor 5 for visibility)

Notes
The script assumes the first column contains grouping labels. Modify the column index if the structure of your input file differs.

Non‑significant correlations (p > 0.05) are set to zero in the output matrix DD but are not used further in PCA (PCA is performed on the normalized data, not on the correlation matrix).

The scaling factor for 3D loading arrows (scale.loads = 5) can be adjusted to improve visual appearance.
