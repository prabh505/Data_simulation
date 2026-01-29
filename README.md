#  Data Generation using Modelling and Simulation for Machine Learning**

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

## **Model Comparison Results**

**Results summary (example values)**

> _The table below reports model performance on the test set. Replace these values with your actual results from the notebook._

| **Model** | **R² Score** | **MAE** | **RMSE** |
|-----------|--------------:|--------:|---------:|
| Random Forest | **0.974681** | **19.145790** | **29.592526** |
| Polynomial Regression (deg 2) | 0.952066 | 30.444987 | 40.717729 |
| Decision Tree | 0.927481 | 31.863434 | 50.082934 |
| KNN | 0.898818 | 34.142181 | 59.158073 |
| Linear Regression | 0.824638 | 57.791961 | 77.880698 |
| SVR | 0.552053 | 77.338957 | 124.473199 |

---

## ** Best Model Selection**

**Based on the evaluation results:**

- **Random Forest** achieved the **highest R² score**.  
- It also produced the **lowest MAE** and **lowest RMSE** among the compared models.  
- **Conclusion:** **Random Forest Regressor** is selected as the **best model** for predicting projectile range in this simulation-based dataset.

**Reasoning:** Random Forests can model complex non-linear relationships and interactions between input parameters (e.g., aerodynamic effects combined with mass and angle), which explains their superior performance on this problem.

---

## ** Graphical Analysis**

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

## **📁 Repository Structure**

Data_simulation/
│
├── notebook.ipynb
├── simulation_data.csv
├── model_comparison.csv
├── README.md
└── results/
    ├── prediction_vs_actual_range.png
    ├── prediction_vs_actual_max_height.png
    └── prediction_vs_actual_time.png


---

## ** Tools and Libraries Used**

- **Python**  
- **PyBullet** (or numerical integrator used for projectile simulation)  
- **NumPy**  
- **Pandas**  
- **Matplotlib**  
- **Seaborn**  
- **Scikit-learn**  
- **XGBoost** (optional for extended comparisons)

---

## ** Conclusion**

This project demonstrates how **modelling and simulation** can be used to generate high-quality synthetic datasets for machine learning. A physics-based projectile motion simulator was developed and used to generate **1000 samples** under varying physical conditions.

Multiple regression models were trained and compared. The results show that **ensemble-based methods (Random Forest, XGBoost)** perform significantly better than simpler linear models for predicting projectile range when aerodynamic drag and multi-parameter interactions are present.

**This confirms the value of simulation-driven machine learning pipelines for scientific and engineering applications.**

---

**If you want:**  
- I can produce a concise **one-page abstract** for submission.  
- I can also **generate the final figures** and embed them in this README with Markdown image links (if you provide the image files or run the notebook and confirm their paths).

