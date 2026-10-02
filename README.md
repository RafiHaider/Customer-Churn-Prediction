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

# 🏅 Executive Summary & Final Lab Report
---

<div style="padding: 15px; background-color: #f8f9fa; border-left: 5px solid #20beff; border-radius: 4px;">
  <h3 style="margin-top:0; color: #111;">🎯 Core Objective</h3>
  <p style="margin-bottom:0;">
    Develop an end-to-end Machine Learning system for <b>Telecom Churn Mitigation</b> by integrating <b>Supervised Model Optimization</b> (XGBoost, Random Forest, Logistic Regression) with <b>Unsupervised Behavioral Intelligence</b> (K-Means Clustering, PCA Dimensionality Reduction).
  </p>
</div>

---

## 📈 Key Technical Deliverables & Benchmarks

### 1. Supervised Learning & Model Engineering
* 🏆 **Top Performing Model:** **Tuned XGBoost** achieved peak predictive power with a 5-Fold Cross-Validation AUC of **0.8504 ± 0.0125**.
* 🎯 **Generalization Verification:** Evaluated **once** on unseen test data, the model achieved a **0.8478 Test AUC**. This falls directly inside the 95% CV confidence interval $[0.8254, 0.8754]$, validating **zero data leakage** and robust out-of-sample stability.
* ⚡ **Optimization Efficiency:** Early stopping converged at **216 trees**, preventing overfitting while maximizing decision boundary precision.

### 2. Unsupervised Clustering & Micro-Segmentation
* 📊 **Optimal Topology ($K=4$):** Balanced mathematical cluster cohesion (Elbow inflection & Silhouette tracking) with actionable commercial utility.
* 🚨 **Critical Risk Segment Identified:** Discovered that **Cluster 1 (*At-Risk High Spenders*)** represents **2,157 customers** driving a massive **43% churn rate**, identifying the primary revenue leak for targeted interventions.

### 3. Dimensionality Reduction & Structural Analysis (PCA)
* 📉 **Variance Compression:** **15 out of 30 principal components** capture 90% of overall dataset variance, proving 50% feature compression capacity.
* 🔍 **Encoding Redundancy Uncovered:** PC1 top loadings ($\approx 0.302$) revealed identical loadings across all `No internet service` categorical dummies, pinpointing strict feature multicollinearity that impacts unregularized linear baselines.

---

## 💡 Commercial Strategy & Retention Matrix

| Cluster ID | Archetype / Segment Name | Customer Count | Avg Tenure | Monthly Spend | Churn Rate | Strategic Business Action |
| :---: | :--- | :---: | :---: | :---: | :---: | :--- |
| **0** | 🛡️ **Budget Long-Termers** | 1,030 | 53.6 mos | $30.96 | **5%** | **Low-Touch Maintenance:** Automated loyalty appreciation & low-cost add-on offers. |
| **1** | 🚨 **At-Risk High Spenders** | 2,157 | 18.4 mos | $80.41 | <span style="color:red; font-weight:bold;">43%</span> | **PRIORITY 1 Intervention:** Proactive success outreach, billing audits, & contract lock-ins. |
| **2** | 💎 **Premium Loyalists** | 1,938 | 59.8 mos | $92.09 | **14%** | **VIP Retention:** Executive support, early feature access, & premium tier perks. |
| **3** | 🌱 **Early Stage Budget** | 1,918 | 9.0 mos | $37.71 | **32%** | **Onboarding Activation:** Targeted feature adoption campaigns & starter bundles. |

---

## 🎓 Academic Conclusion

This project demonstrates that predictive analytics reaches maximum efficacy when **high-capacity ensemble classifiers** are coupled with **unsupervised behavioral profiling**. While hyperparameter tuning optimized decision boundary precision (+0.005 AUC gain), PCA and K-Means provided the structural domain insights necessary to turn raw churn predictions into targeted revenue preservation strategies.

> **Model Artifact Status:** Saved & Serialized as `churn_model.joblib`
