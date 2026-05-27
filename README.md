# Statistical Analysis of Student Academic Outcomes

A statistical analysis of the UCI *Predict Students' Dropout and Academic Success* dataset (4,424 students from a Portuguese higher education institution). The project covers eight analyses: distribution and outlier inspection, correlation analysis, Fisher Distance, PCA, LDA, four clustering methods (K-Means, DBSCAN, t-SNE, SOM), and a hypothesis test with power analysis.

**Author:** Nashit · Gebze Technical University, Department of Computer Engineering

## Key findings

- **Academic performance dominates everything else.** The four highest-Fisher-Distance features are all curricular performance variables. 2nd-semester units approved alone gives F = 1.22, followed by 1st-semester approved (0.86) and the two semester grades (0.69, 0.45). Everything else sits below 0.13.
- **Age at enrollment is the strongest non-academic predictor.** Dropouts average 24.6 years vs Graduates at 20.7 years, a 3.9-year gap with $p < 10^{-77}$.
- **Macroeconomic features are noise at the individual level.** Unemployment, inflation, and GDP all have Fisher Distance below 0.001.
- **The Enrolled class is intrinsically transitional.** All four clustering methods recover a clear Dropout-to-Graduate gradient but none isolates Enrolled as its own cluster. LDA silhouette is 0.224, well below the 0.5 threshold for well-defined clusters.
- **LDA beats PCA by 2.34× on Fisher Distance and 3.2× on silhouette** in 2D, as theory predicts.

## Repository contents

| File | Description |
|---|---|
| `Final_Project_Notebook.ipynb` | Complete executed notebook, 8 tasks, 17 plots embedded |
| `student_success.csv` | UCI dataset (4,424 rows × 37 columns) |
| `paper/main.tex` | IEEE-format paper |
| `paper/main.pdf` | Compiled paper |
| `paper/figures/` | All figures used in the paper |

## Running the notebook

```bash
pip install numpy pandas matplotlib seaborn scipy scikit-learn MiniSom jupyter
jupyter notebook Final_Project_Notebook.ipynb
```

Place `student_success.csv` in the same directory as the notebook. Full execution takes 1-2 minutes (t-SNE is the slowest step at around 20 seconds).

## Methodology highlights

- **Feature-aware IQR cleaning.** A naive row-drop rule discards 74% of the Dropout class because of zero-inflated features. The three-tier procedure used here (winsorize Age, exclude six degenerate features from the row-drop decision, apply standard IQR cleaning to the remaining eleven) retains 84% of rows and preserves class balance across all three classes.
- **Fisher-ANOVA equivalence verified.** For all 18 features, $F^{\text{ANOVA}} / F^{\text{Fisher}} = 1866.5 = (N-C)/(C-1)$ at machine precision, confirming the implementation.
- **Power analysis on a moderate-effect feature.** 1000-trial repeated sampling shows the empirical rejection rate rises from 87.2% at $n=36$ to 98.8% at $n=64$.

## Dataset

Realinho, V., Machado, J., Baptista, L., and Martins, M. V. (2022). *Predicting Student Dropout and Academic Success*. Data 7(11):146. [doi.org/10.3390/data7110146](https://doi.org/10.3390/data7110146)

## License

The dataset is distributed by UCI Machine Learning Repository under CC BY 4.0. Analysis code in this repository is provided as-is for academic use.
