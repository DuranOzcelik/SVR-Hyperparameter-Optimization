SVR Hyperparameter Optimization

Author: Duran Özçelik

📋 Project Overview
This project implements Support Vector Machine Regression (SVR) on the California Housing dataset with hyperparameter optimization using GridSearchCV and RandomizedSearchCV. The Project is  focusing on comparing different hyperparameter search strategies and evaluating their effectiveness in finding optimal model parameters.

🎯 Objectives

* Train and evaluate SVR models with different kernel types (linear and RBF)
* Implement GridSearchCV for systematic hyperparameter search
* Implement RandomizedSearchCV for random hyperparameter sampling
* Compare both search strategies in terms of performance and efficiency
* Find optimal hyperparameters for housing price prediction
* Analyze RMSE scores and identify the best model configuration

🛠️ Technologies Used

* Python 3.12 - Core programming language
* NumPy - Numerical computations and array operations
* Pandas - Data manipulation and analysis
* Scikit-Learn - Machine learning algorithms and model selection tools
* Matplotlib - Data visualization and plotting
* SciPy - Statistical distributions for RandomizedSearchCV
* Jupyter Notebook - Interactive development environment

📊 Dataset
**California Housing Dataset**
The dataset contains information about housing districts in California from the 1990 census:

* **Size:** 20,640 instances
* **Features:** 9 total (8 numerical + 1 categorical)

**Feature Descriptions:**

* longitude - Longitude coordinate
* latitude - Latitude coordinate
* housing_median_age - Median age of houses in the district
* total_rooms - Total number of rooms in the district
* total_bedrooms - Total number of bedrooms in the district
* population - District population
* households - Number of households in the district
* median_income - Median income of households (in tens of thousands)
* ocean_proximity - Categorical variable (proximity to ocean)

**Target Variable:** median_house_value - Median house value in the district
**Missing Values:** 207 districts have missing total_bedrooms values

🔍 Methodology

1. **Data Preparation**

   * **Data Loading and Exploration:** Loaded dataset, explored data distributions, identified missing values.
   * **Train-Test Split:** Stratified sampling based on income categories (5 strata). 80% training set, 20% test set.
   * **Feature Engineering:** Created income categories for stratification, separated numerical and categorical features.
   * **Data Preprocessing Pipeline:**

     * Missing Value Imputation: *SimpleImputer* (median)
     * Feature Scaling: *StandardScaler*
     * Categorical Encoding: *OneHotEncoder*
     * Final feature count: 13 features

2. **GridSearchCV Implementation**

   * **Hyperparameter Grid:**

     * Linear Kernel: C = [0.1, 1, 10, 100, 1000]
     * RBF Kernel: C = [0.1, 1, 10, 100, 1000], Gamma = ['scale', 'auto', 0.001, 0.01, 0.1, 1]
   * **Cross-Validation:** 3-fold, scoring = negative MSE
   * **Total Models:** 105
   * **Results:** Best RMSE = $70,602.93 | Kernel: linear | C: 1000

3. **RandomizedSearchCV Implementation**

   * **Parameter Distributions:**

     * Kernel: ['linear', 'rbf']
     * C: Log-uniform(0.1, 1000)
     * Gamma: Log-uniform(0.001, 1)
   * **Iterations:** 50, **CV:** 3-fold
   * **Results:** Best RMSE = $70,627.34 | Kernel: linear | C: 856.886979

📈 Results Summary

| Metric         | GridSearchCV | RandomizedSearchCV | Difference     |
| -------------- | ------------ | ------------------ | -------------- |
| Best RMSE      | $70,602.93   | $70,627.34         | $24.41 (0.03%) |
| Best Kernel    | linear       | linear             | Same           |
| Best C         | 1000         | 856.89             | Different      |
| Models Trained | 105          | 150                | +45            |

**Key Findings:**

* Minimal performance difference (0.03%) between methods
* Both favored **linear kernel** and **high C** values
* GridSearchCV slightly better RMSE but fewer combinations
* RMSE ≈ $70,600 ≈ 14-18% relative error

🚀 Installation & Usage

1. **Install Dependencies:**

```bash
pip install numpy pandas scikit-learn matplotlib scipy jupyter
```

2. **Run Notebook:**

```bash
jupyter notebook
```

3. **Execute Cells:** Run all cells in `BIM453_HW1_Solution.ipynb`

**Expected Output:**

* Data loading and preprocessing summary
* Progress bars during training
* Best RMSE and parameters for both methods
* Comparison table of results

🔑 Key Insights

* **Model Performance:** RMSE ≈ $70,600 — reasonable accuracy for housing data.
* **GridSearchCV:** Best for final fine-tuning.
* **RandomizedSearchCV:** Faster, better for large search spaces.
* **Recommendation:** Use RandomizedSearchCV for exploration, GridSearchCV for precise optimization.

📚 References

* Géron, A. (2022). *Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow* (3rd ed.). O'Reilly Media.
* Scikit-Learn Documentation: [https://scikit-learn.org/stable/](https://scikit-learn.org/stable/)
* California Housing Dataset: StatLib Repository (via Ageron’s GitHub)
* Bergstra, J., & Bengio, Y. (2012). *Random search for hyper-parameter optimization.* Journal of Machine Learning Research.
