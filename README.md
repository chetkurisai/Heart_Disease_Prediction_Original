Step 1: Medallion Architecture – Data Engineering
We implemented the Medallion Architecture (Bronze → Silver → Gold) to ensure scalable, modular, and clean data processing for the heart disease prediction system. This approach separates raw data ingestion from cleaning and feature engineering, improving data traceability and maintainability.

Bronze Layer – Raw Data Ingestion
Purpose: Stores raw heart disease data ingested from the UCI dataset without any modifications.

Details:
Contains all original columns and unprocessed entries.
Acts as the source of truth for audits and recovery.
Silver Layer – Cleaned & Validated Data
Purpose: Stores cleaned and validated data for further processing.

Transformations Applied:
Handled missing or null values.
Converted data types as required.
Removed duplicates and invalid records.
Normalized/standardized column names for consistency.

Gold Layer – Model-Ready Data
Purpose: Final curated dataset used for model training and evaluation.

Enhancements:
Created a new binary target column based on heart disease presence.
Dropped irrelevant columns such as patient ID or dataset index.
Preserved only medically meaningful features to support predictive modeling.
Ensured label encoding or transformation where needed.

MongoDB Collections
Each layer is stored in a separate MongoDB Atlas collection for modular access:
heart_disease_bronze
heart_disease_silver
heart_disease_gold1

Summary
The Medallion Architecture helped isolate responsibilities between raw ingestion, cleaning, and modeling readiness. It also ensured that:
No transformation logic is mixed across layers.
Each step is traceable and reusable.
Data quality is systematically improved.

Step 2: Final Model Development Summary for Documentation
Model Development
We developed multiple classification models to predict heart disease using cleaned and preprocessed data from the Gold layer in MongoDB.

Data Source
Data was loaded from the heart_disease_gold collection in MongoDB Atlas.


The target column was derived by converting the num field:

target = 1 if num > 0 (presence of heart disease)
target = 0 otherwise
Target Variable
target: Binary classification (0 = no disease, 1 = disease)

Models Trained
Logistic Regression
Random Forest
XGBoost
Support Vector Machine (SVM)

Evaluation Metrics
Each model was evaluated on:
Accuracy
Precision
Recall
F1 Score
ROC-AUC

Final Model Selection
Random Forest performed best based on F1 Score and ROC-AUC.
This model was chosen as the final model for deployment.

Feature Selection
Dropped non-informative columns: id, dataset, num

Kept all medically relevant features based on domain knowledge (e.g., cp, chol, thalach, etc.)

Hyperparameter Tuning
Default hyperparameters were used initially.
Advanced tuning (e.g., Grid Search) can be added in future improvements.

Model Saving
Final model (Random Forest) saved as:
heart_disease_model.pkl
Saved using joblib.dump() in the working directory.





