# OTU Niche Breadth vs. Relative Abundance Analysis

This repository contains a Python script for the quantitative analysis and visualization of microbial ecological patterns, focusing on the relationship between **OTU niche breadth** (Levins' Bi) and **mean relative abundance**. This type of analysis is frequently used in microbial ecology, environmental microbiome studies, and functional diversity assessments.

---

##  Objective

The primary aim is to assess whether microbial taxa with broader ecological distributions (i.e., higher niche breadth) tend to exhibit higher or lower average abundance, and how these patterns differ between predefined experimental groups (e.g., treatment vs. control, high vs. low nutrient conditions).

---

##  Input

- **OTU abundance table** (`otu_copies.csv`)  
  A comma-separated file where:
  - Rows correspond to individual OTUs
  - Columns correspond to sample names
  - First column should be `#OTU ID`
  - Remaining columns are absolute abundance values

---

##  Workflow Overview

1. **Group Definition**:  
   Two sample groups (e.g., `high` and `low`) are defined manually in the script.

2. **Relative Abundance Calculation**:  
   OTU abundances are normalized within each sample to obtain relative abundances.

3. **Niche Breadth Estimation**:  
   Levins' niche breadth index is computed per OTU using the formula:

   \[
   B_i = \frac{1}{\sum_{j} p_{ij}^2}
   \]

   where \( p_{ij} \) is the relative abundance of OTU *i* in sample *j*.

4. **Data Aggregation**:  
   For each group, mean relative abundance and niche breadth are calculated per OTU.

5. **Joint Visualization**:  
   A scatterplot of niche breadth (y-axis) vs. log₁₀-transformed mean relative abundance (x-axis) is generated, with group-level KDE density plots shown on the top and right margins.

6. **Figure Export**:  
   The output figure is saved as a high-resolution, vectorized, fully editable PDF (`otu_niche_plot.pdf`) for downstream academic use.

---

##  Output

- `otu_niche_plot.pdf`  
  A publication-quality figure containing:
  - Central scatter plot of OTUs colored by group
  - Marginal density plots of Bi and log₁₀ abundance
  - Adjustable axes ranges and styling
  - Editable in Adobe Illustrator, Inkscape, etc.

---

##  Usage Instructions

### Step 1. Install dependencies:

```bash
pip install pandas numpy matplotlib seaborn
````

### Step 2. Modify the script:

* Set the correct path to your OTU abundance table:

  ```python
  file_path = r"your_path_to/otu_copies.csv"
  ```

* Define your sample groupings:

  ```python
  high_samples = ["sample1", "sample2"]
  low_samples = ["sample3", "sample4"]
  ```

### Step 3. Run the script:

```bash
python otu_niche_plot.py
```

### Step 4. Locate output figure:

* The file `otu_niche_plot.pdf` will be saved in the current working directory.
* Use vector graphic editors to further customize as needed.

---

##  Suggested Further Analyses

* **Statistical comparison** of Bi values across groups (e.g., Mann–Whitney U test)
* **Correlation analysis** between niche breadth and abundance (e.g., Spearman ρ)
* **Functional annotation** of OTUs with extreme niche profiles
* **Environmental association** via redundancy analysis (RDA), NMDS, or machine learning models

---
