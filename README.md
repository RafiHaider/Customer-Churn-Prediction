# Customer Churn Prediction 
## Week 1: Exploratory Data Analysis  
### Dataset 
- Source: Telco Customer Churn (Kaggle)
- Size: 7,043 customers, 21 features
- Target: Predict customer churn (Yes/No)
### Key Findings   
- **Overall Churn Baseline:** Approximately **26.5%** of overall customers churned, establishing a target baseline for predictive modeling.
- **Contract Type Impact:** Customers on **Month-to-month contracts** exhibit a significantly higher churn rate compared to those on 1-year or 2-year commitments.
- **Tenure Risk Window:** New customers with **tenure < 12 months** are at the highest risk of leaving; retention stabilizes noticeably as tenure increases.
- **High-Risk Segments:** Users subscribed to **Fiber Optic internet** and those paying via **Electronic Check** show the highest rates of churn.
- **Service Add-ons:** Customers who lack support add-ons, such as **Online Security** or **Tech Support**, churn at a higher rate than those with active security services.

# Week 2: Building ML Models
- Baseline (always "stay"): accuracy 73.5%
- Best model: Logistic Regression, AUC 0.842, recall >85% at threshold t = 0.15
- Top churn drivers (permutation importance): tenure, TotalCharges, Contract_Two year
- Threshold chosen: t = 0.15, because lowering the classification threshold minimizes asymmetric business costs by capturing high-risk churners early before they cancel service
- Engineered features: n_services, is_new, charge_per_mo, price_jump; effect on AUC: 0.8422 -> 0.8420
- Biggest lesson: Tree-based ensemble models naturally capture non-linear feature interactions without manual feature engineering, making cost-sensitive threshold optimization on well-calibrated probabilities the most effective leverage point for improving business value.

