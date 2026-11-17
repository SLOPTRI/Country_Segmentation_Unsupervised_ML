# Country Segmentation with K-means

Can countries with similar health, economic, and trade indicators be grouped without predefined labels? This project uses K-means to explore patterns across **167 countries** and tests whether a smaller set of indicators can preserve the main country profiles.

[Open the Jupyter notebook](main.ipynb)

## Dataset

The analysis uses the [Unsupervised Learning on Country Data dataset](https://www.kaggle.com/datasets/rohan0301/unsupervised-learning-on-country-data) from Kaggle.

Country names are kept to identify observations in the results. The `inflation` column is excluded because its definition in the data dictionary is ambiguous.

## Methodology

1. **Explore the data.** Check for missing values and duplicates, inspect distributions, and examine correlations between indicators.
2. **Compare two sets of indicators.** The full model uses eight indicators. The reduced model drops `income` and `total_fer` to test whether the main profiles remain visible with fewer correlated features. Both sets are standardized with `StandardScaler` before clustering.
3. **Choose the number of clusters.** Test two to six clusters using the silhouette score. Four clusters give the highest score for both sets within this range.
4. **Interpret the clusters.** Match clusters by the countries they share, compare median indicator values in their original units, and visualize both models on the same two-dimensional PCA projection.

## Results

| Model | Indicators | Clusters | Silhouette score |
| --- | ---: | ---: | ---: |
| Full | 8 | 4 | 0.334 |
| Reduced | 6 | 4 | 0.317 |

I chose the **reduced model**. Its silhouette score is slightly lower, but it preserves the four broad profiles with two fewer indicators. After matching the cluster labels, both models assign **158 of 167 countries (94.61%)** to corresponding groups. This percentage measures agreement between the models; the dataset has no ground-truth labels for calculating accuracy.

Three clusters broadly differ in GDP per capita, child mortality, and life expectancy. The fourth contains **Luxembourg, Malta, and Singapore** in both models. What stands out about this group is its trade: median exports and imports are **175%** and **154%** of GDP, respectively.

The final model uses **child mortality, exports, health spending, imports, life expectancy, and GDP per capita**. The results describe patterns in this dataset and depend on which indicators are included and how they are scaled.

## Run locally

1. Clone or download this repository.
2. Install the Python dependencies:

   ```bash
   python -m pip install jupyter pandas matplotlib seaborn scikit-learn
   ```

3. If the dataset is missing, download it from Kaggle and place `Country-data.csv` at `archive/Country-data.csv`, relative to the repository root.
4. From the repository root, open `main.ipynb` in Jupyter and run the cells in order.

Developed as an NF3 project for the *Machine Learning Systems* course in the *Artificial Intelligence and Big Data* specialization.