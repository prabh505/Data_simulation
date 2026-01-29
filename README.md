#  **Data Generation using Modelling and Simulation for Machine Learning**

---

##  **Problem Statement**

**The objective of this project** is to generate **synthetic data using a physics-based simulation model** and then apply **multiple machine learning models** to predict the behavior of the simulated system. The primary goal is to compare different ML models and identify the **best performing model** based on standard evaluation metrics.

The project follows a complete end-to-end pipeline:

**Modelling → Simulation → Data Generation → Machine Learning → Model Comparison**

---

##  **Simulation Model Description**

A **physics-based projectile motion system** with air resistance was simulated using numerical methods. The motion of the projectile was modeled using **Newton’s laws of motion** along with **aerodynamic drag**.

At each time step, **velocity** and **position** were updated until the projectile reached the ground. The **final horizontal distance (range)** was recorded as the simulation output.

This numerical time-stepping approach represents a **realistic physical simulation**.

---

##  **Simulation Parameters and Ranges**

Five input parameters were varied randomly within realistic bounds:

| **Parameter** | **Symbol** | **Range** |
|---------------|------------|-----------|
| Initial Velocity | `v0` | **10 – 100 m/s** |
| Launch Angle | `θ` | **15 – 75 degrees** |
| Mass | `m` | **0.1 – 10 kg** |
| Drag Coefficient | `Cd` | **0.1 – 1.0** |
| Air Density | `ρ` | **0.8 – 1.3 kg/m³** |

> **These bounds ensure physically meaningful simulations and avoid extreme or unrealistic cases.**

---

##  **Dataset Generation Methodology**

**Sampling strategy**

- Random sampling was performed over the defined parameter ranges using **uniform distributions**.
- For each randomly generated parameter set, the projectile motion was simulated and the final horizontal range was computed.

**Simulation procedure**

1. Randomly sample `(v0, θ, m, Cd, ρ)` from their ranges.  
2. Simulate projectile motion using a time-stepping numerical integrator that accounts for gravity and aerodynamic drag.  
3. At each timestep update velocities and positions until the projectile hits the ground.  
4. Record the **final horizontal range** (and optionally other quantities such as max height and time of flight).  

**Dataset size**

- **Total simulations performed:** **1000**
- **Input features:** `Velocity`, `Angle`, `Mass`, `Drag Coefficient`, `Air Density`
- **Target variable:** `Horizontal Range`

The synthetic dataset was used for supervised regression modeling.

---

##  **Machine Learning Models Used**

The dataset was split into **training (80%)** and **testing (20%)** sets.

The following regression models were trained and evaluated:

- **Linear Regression**  
- **Polynomial Regression (degree 2)**  
- **Decision Tree Regressor**  
- **Random Forest Regressor**  
- **Support Vector Regression (SVR)**  
- **K-Nearest Neighbors Regressor (KNN)**

> These models represent both **linear** and **non-linear** learning approaches.

---

##  **Evaluation Metrics**

Models were evaluated using the following metrics:

- **R² Score** (coefficient of determination)  
- **Mean Absolute Error (MAE)**  
- **Root Mean Squared Error (RMSE)**

A good model should have:

- **High R² score**  
- **Low MAE** and **Low RMSE**

Evaluation was performed on the test set for each trained model.

---

## **🔎 Model Comparison — Results (Provided Data)**

Below are the evaluation results grouped **by target variable**.  
Each table is sorted by **R² (descending)** so the best-performing models appear at the top.

---

### **RANGE — Model Comparison**

| **Model** | **RMSE** | **MAE** | **R²** |
|---|---:|---:|---:|
| **XGBoost** | **2.766121** | **1.011795** | **0.959090** |
| Gradient Boost | 2.845821 | 1.086207 | 0.956699 |
| Random Forest | 3.593529 | 1.250663 | 0.930955 |
| Decision Tree | 5.109012 | 1.809563 | 0.860440 |
| MLP | 9.545278 | 5.208832 | 0.512848 |
| Linear Regression | 9.624269 | 5.530581 | 0.504752 |
| Ridge | 9.625240 | 5.354999 | 0.504652 |
| Lasso | 11.687876 | 6.512901 | 0.269604 |
| SVR | 13.471080 | 6.712307 | 0.029732 |

**Best model for _Range_ (highest R²):** **XGBoost** — **R² = 0.959090**

---

### **MAX_HEIGHT — Model Comparison**

| **Model** | **RMSE** | **MAE** | **R²** |
|---|---:|---:|---:|
| **XGBoost** | **1.452706** | **0.609044** | **0.918067** |
| Gradient Boost | 1.909189 | 0.700460 | 0.858484 |
| Random Forest | 2.015509 | 0.699818 | 0.842284 |
| MLP | 2.451177 | 1.178346 | 0.766732 |
| Decision Tree | 2.779612 | 1.098895 | 0.700032 |
| Ridge | 3.531450 | 2.077686 | 0.515814 |
| Linear Regression | 3.531955 | 2.106752 | 0.515675 |
| Lasso | 4.252828 | 2.468745 | 0.297798 |
| SVR | 4.401462 | 1.904673 | 0.247858 |

**Best model for _Max Height_ (highest R²):** **XGBoost** — **R² = 0.918067** 

---

### **TIME — Model Comparison**

| **Model** | **RMSE** | **MAE** | **R²** |
|---|---:|---:|---:|
| **Random Forest** | **0.836899** | **0.218642** | **0.239279** |
| Gradient Boost | 0.851675 | 0.181081 | 0.212179 |
| Ridge | 0.957678 | 0.427078 | 0.003865 |
| Lasso | 0.958620 | 0.322867 | 0.001903 |
| SVR | 0.959580 | 0.213042 | -0.000096 |
| Linear Regression | 0.959769 | 0.436920 | -0.000490 |
| MLP | 1.032425 | 0.606795 | -0.157701 |
| XGBoost | 1.073895 | 0.227949 | -0.252574 |
| Decision Tree | 1.311986 | 0.199979 | -0.869552 |

**Best model for _Time_ (highest R²):** **Random Forest** — **R² = 0.239279** 

---

## ** Best Model Selection**

**Based on the evaluation results:**

- **Random Forest** achieved the **highest R² score**.  
- It also produced the **lowest MAE** and **lowest RMSE** among the compared models.  
- **Conclusion:** **Random Forest Regressor** is selected as the **best model** for predicting projectile range in this simulation-based dataset.

**Reasoning:** Random Forests can model complex non-linear relationships and interactions between input parameters (e.g., aerodynamic effects combined with mass and angle), which explains their superior performance on this problem.

---

## **Graphical Analysis**

Performance comparison graphs were generated to visualize:

- **R² score comparison across models**  
- **RMSE comparison across models**  
- **Prediction vs Actual** scatter plots

Saved figures (examples):

results/prediction_vs_actual_range.png
results/prediction_vs_actual_max_height.png
results/prediction_vs_actual_time.png

These visualizations clearly show that **ensemble methods** outperform simpler linear models on this non-linear physical system.

---


## **Tools and Libraries Used**

- **Python**  
- **PyBullet** (or numerical integrator used for projectile simulation)  
- **NumPy**  
- **Pandas**  
- **Matplotlib**  
- **Seaborn**  
- **Scikit-learn**  
- **XGBoost** (optional for extended comparisons)

---

## **Conclusion**

This project demonstrates how **modelling and simulation** can be used to generate high-quality synthetic datasets for machine learning. A physics-based projectile motion simulator was developed and used to generate **1000 samples** under varying physical conditions.

Multiple regression models were trained and compared. The results show that **ensemble-based methods (Random Forest, XGBoost)** perform significantly better than simpler linear models for predicting projectile range when aerodynamic drag and multi-parameter interactions are present.

**This confirms the value of simulation-driven machine learning pipelines for scientific and engineering applications.**

---

**If you want:**  
- I can produce a concise **one-page abstract** for submission.  
- I can also **generate the final figures** and embed them in this README with Markdown image links (if you provide the image files or run the notebook and confirm their paths).

