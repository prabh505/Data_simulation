Data Generation using Modelling and Simulation for Machine Learning
🔍 Problem Statement

The objective of this project is to generate synthetic data using a physics-based simulation model and then apply multiple machine learning models to predict the behavior of the simulated system. The primary goal is to compare different ML models and identify the best performing model based on standard evaluation metrics.

The project follows a complete end-to-end pipeline:

Modelling → Simulation → Data Generation → Machine Learning → Model Comparison

⚙️ Simulation Model Description

A physics-based projectile motion system was simulated using the PyBullet physics engine. The motion of a spherical object was governed by Newton’s laws of motion, including:

Gravitational force

Air resistance (linear damping)

Collision with the ground

Variable mass and restitution

At each time step, the simulator numerically updated the object’s velocity and position until it reached the ground. From the full trajectory, the following outputs were recorded:

Maximum height achieved

Horizontal distance travelled (range)

Total time of flight

This time-stepping numerical simulation represents a realistic physical modelling approach widely used in engineering and robotics.

🧪 Simulation Parameters and Ranges

The following physical parameters were varied randomly within realistic bounds:

Parameter	Description	Range
mass	Object mass (kg)	0.1 – 10
velocity	Initial velocity (m/s)	5 – 50
angle	Launch angle (degrees)	10 – 80
drag	Air resistance (linear damping)	0.0 – 0.5
gravity	Gravity (m/s²)	5 – 15
restitution	Surface bounciness	0.1 – 0.9

These bounds ensure physically meaningful simulations while avoiding unstable or unrealistic conditions.

🗃️ Dataset Generation Methodology

Random sampling was performed over all defined parameter ranges using uniform distributions.

For each randomly generated parameter set:

Parameters were passed to the PyBullet simulator

The projectile motion was simulated

Physical outputs were recorded

A total of 1000 independent simulations were executed, producing a synthetic dataset with:

✅ Input Features

Mass

Velocity

Angle

Drag coefficient

Gravity

Restitution

🎯 Target Variables

Maximum height

Horizontal range

Time of flight

The generated dataset is stored as:

simulation_data.csv


This dataset was then used for supervised regression modelling.

🤖 Machine Learning Models Used

Each output variable was treated as an independent regression problem.

The dataset was split into:

80% training

20% testing

The following models were trained and evaluated:

Linear Regression

Ridge Regression

Lasso Regression

Decision Tree Regressor

Random Forest Regressor

Gradient Boosting Regressor

Support Vector Regressor (SVR)

Multi-Layer Perceptron (Neural Network)

XGBoost Regressor

These models include linear, non-linear, ensemble, and neural approaches, enabling a strong comparative study.

📊 Evaluation Metrics

Each model was evaluated using:

R² Score (coefficient of determination)

Mean Absolute Error (MAE)

Root Mean Squared Error (RMSE)

A good model should demonstrate:

High R² score

Low MAE

Low RMSE

Evaluation was performed separately for each target variable.

📈 Model Comparison Results

The full evaluation results are saved in:

model_comparison.csv


Models are grouped and ranked for:

Range prediction

Maximum height prediction

Time of flight prediction

Across all targets, ensemble models (XGBoost, Random Forest, Gradient Boosting) consistently achieved the best performance, indicating their strong capability in modelling non-linear physical systems.

🏆 Best Model Selection

Based on the quantitative evaluation:

They also produced the lowest MAE and RMSE

XGBoost and Random Forest were consistently top performers

These models are selected as the best predictors for projectile behavior due to their ability to capture complex interactions between physical parameters.

📉 Graphical Analysis

Performance comparison graphs were generated and saved in the results/ directory to visualize:

R² comparison across models

Prediction vs actual values

Correlation between features and targets

Saved figures include:

prediction_vs_actual_range.png  
prediction_vs_actual_max_height.png  
prediction_vs_actual_time.png  


These visualizations clearly show that ensemble models outperform simpler linear approaches.

📁 Repository Structure
Data_simulation/
│
├── notebook.ipynb
├── simulation_data.csv
├── model_comparison.csv
├── README.md
└── results/
    ├──
    ├── prediction_vs_actual_range.png
    ├── prediction_vs_actual_max_height.png
    └── prediction_vs_actual_time.png

🧰 Tools and Libraries Used

Python

PyBullet

NumPy

Pandas

Matplotlib

Seaborn

Scikit-learn

XGBoost


🏁 Conclusion

This project demonstrates how modelling and simulation can be effectively used to generate synthetic datasets for machine learning. A physics-based projectile motion simulator was developed using PyBullet and used to generate 1000 samples under varying physical conditions.

Multiple regression models were trained and compared. The results clearly show that ensemble-based machine learning methods significantly outperform simpler models when dealing with complex physical systems.

This confirms the value of simulation-driven machine learning pipelines for scientific and engineering applications.
