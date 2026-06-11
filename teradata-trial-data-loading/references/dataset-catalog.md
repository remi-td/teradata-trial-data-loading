# Teradata ClearScape Demo Dataset Catalog

All datasets are available in `_local` and `_cloud` variants unless noted.
Use `_local` for best query performance. Use `_cloud` to avoid consuming local perm space.

---

## 🏥 Healthcare

| Dataset Name | Description |
|---|---|
| `DEMO_HealthcareFWA` | Fraud, Waste & Abuse detection in healthcare claims |
| `DEMO_HealthcareFWA_VA` | Healthcare FWA variant (local only) |
| `DEMO_HealthcareSW` | Healthcare patient data for survival/outcome analysis |
| `DEMO_HealthcareCOC` | Continuity of Care patient journey data |
| `DEMO_HeathcareCOC` | Alternate COC variant (cloud only) |
| `DEMO_HospitalReadmission` | Patient readmission prediction dataset |
| `DEMO_HeartFailure` | Heart failure clinical records for prediction modeling |
| `DEMO_CancerPrediction` | Cancer diagnosis classification dataset |
| `DEMO_DiabetesPrediction` | Diabetes prediction (standard and BYOM variant) |
| `DEMO_DiabetesPrediction_BYOM` | Diabetes prediction with Bring Your Own Model (local only) |
| `DEMO_ParkinsonsDisease` | Parkinson's disease biomedical voice data (local only) |
| `DEMO_KneeReplacement` | Knee replacement patient outcomes |
| `DEMO_Health` | General health/patient dataset |
| `DEMO_Medical` | Medical records and treatment data |
| `DEMO_SurvivalAnalysis` | Time-to-event survival analysis dataset |

---

## 🏦 Financial / Banking

| Dataset Name | Description |
|---|---|
| `DEMO_BankChurn` | Bank customer churn prediction |
| `DEMO_BankChurnIVSM` | Bank churn using In-Vantage Scoring Models |
| `DEMO_Bank` | General banking dataset |
| `DEMO_Banking` | Extended banking/transaction data (cloud only) |
| `DEMO_CreditCard` | Credit card transactions and fraud detection |
| `DEMO_CreditRisk` | Credit risk scoring dataset |
| `DEMO_Financial` | Financial instruments and market data |
| `DEMO_GLM_Fraud` | Fraud detection using Generalized Linear Models |
| `DEMO_Insurance` | Insurance claims and policy data (local only) |

---

## 🛍️ Retail / Commerce / Marketing

| Dataset Name | Description |
|---|---|
| `DEMO_Retail` | Retail sales transactions |
| `DEMO_RetailJourney` | Customer retail journey / path-to-purchase |
| `DEMO_Grocery_Data` | Grocery store transaction data |
| `DEMO_Advertising` | Digital advertising campaign data |
| `DEMO_MultiTouchAttribution` | Marketing attribution across touchpoints |
| `DEMO_MarketingCamp` | Marketing campaign response data |
| `DEMO_ProductHierarchy` | Product taxonomy and hierarchy data |
| `DEMO_CustomerReviews` | Customer text reviews for NLP/sentiment |
| `DEMO_FoodReviews` | Food product reviews for NLP analysis |
| `DEMO_Customer360` | 360-degree customer profile dataset |
| `DEMO_Cust_Travel` | Customer travel behavior data |
| `DEMO_DigitalEvents` | Digital clickstream / web event data |

---

## 📡 Telco / IoT / 5G

| Dataset Name | Description |
|---|---|
| `DEMO_Telco` | Telecom customer churn and usage data |
| `DEMO_TelcoNetwork` | Network performance and fault data |
| `DEMO_Telco_Complaints` | Telecom customer complaint text data |
| `DEMO_Telco_Complaints_Onnx` | Telco complaints with ONNX model scoring |
| `DEMO_5G` | 5G network analytics dataset |
| `DEMO_5G_test` | 5G test variant (cloud only) |
| `DEMO_IndoorSensor` | IoT indoor sensor time-series data |
| `DEMO_EVCarBattery` | Electric vehicle battery telemetry |
| `DEMO_Energy` | Energy consumption and production data |

---

## 🚕 Transportation / Urban / Environment

| Dataset Name | Description |
|---|---|
| `DEMO_AustinBikeShare` | Austin bike share trips, stations, and weather data |
| `DEMO_NYCTaxi` | New York City taxi trip records |
| `DEMO_TrainDelay` | Train delay prediction dataset |
| `DEMO_AirPassengers` | Classic airline passenger time-series |
| `DEMO_NZFloods` | New Zealand flood event geospatial data |

---

## 🤖 ML / AI / Data Science

| Dataset Name | Description |
|---|---|
| `DEMO_AnomalyDetection` | Anomaly detection dataset (standard and EFS variants) |
| `DEMO_AnomalyDetection_EFS` | Anomaly detection with external feature store |
| `DEMO_DataAnomaly` | Data-level anomaly detection |
| `DEMO_DataImbalance` | Imbalanced classification dataset for resampling demos |
| `DEMO_ModelOps` | MLOps / model lifecycle management dataset |
| `DEMO_NLP` | Natural language processing corpus |
| `DEMO_SLM_RAG` | Small language model RAG (retrieval-augmented generation) |
| `DEMO_SLMRAG_Catalogue` | RAG catalogue/index dataset (local only) |
| `DEMO_LLM_FineTuning` | LLM fine-tuning dataset (cloud only) |
| `DEMO_DataScienceExploration` | General data science exploration dataset |
| `DEMO_DataScienceFlow` | End-to-end data science pipeline dataset |
| `DEMO_HyperModel` | Hyperparameter tuning / AutoML dataset |
| `DEMO_FeatureEngg` | Feature engineering examples (local only) |
| `DEMO_ResumeClassification` | Resume/CV text classification (local only) |
| `DEMO_Hashing` | Data hashing and privacy techniques dataset |
| `DEMO_Entity_Resolution` | Record linkage / entity resolution dataset |
| `DEMO_ComplaintAnalysis` | Complaint text analysis and classification |
| `DEMO_Sonar` | Sonar signal classification (classic ML benchmark) |
| `DEMO_Secom` | Semiconductor manufacturing defect detection |

---

## 📊 Forecasting / Time Series

| Dataset Name | Description |
|---|---|
| `DEMO_SalesForecasting` | Sales forecasting time series |
| `DEMO_SalesForecastingUAF` | Sales forecasting using Univariate Analysis Functions |
| `DEMO_SlsForecast_SAS` | Sales forecasting with SAS integration |
| `DEMO_DemandForecast` | Demand forecasting dataset |
| `DEMO_ProphetSTO` | Time series forecasting using Prophet-style models |
| `DEMO_UAF` | Univariate Analysis Functions reference dataset |
| `DEMO_SalesOffload` | Sales data offload/archival use case |

---

## 🏭 Manufacturing / Operations

| Dataset Name | Description |
|---|---|
| `DEMO_GreenManufacturing` | Sustainable/green manufacturing metrics |
| `DEMO_PredictiveMaintenance` | Equipment failure prediction (IoT sensor data) |
| `DEMO_RemaingUsefulLife` | Remaining Useful Life (RUL) prediction for equipment |
| `DEMO_Inventory` | Inventory management and optimization |
| `DEMO_SupplyChain` | Supply chain logistics data (local only) |
| `DEMO_ShippingTimePrediction` | Shipping/delivery time prediction (local only) |
| `DEMO_ESG` | Environmental, Social & Governance metrics |

---

## 📈 Graph / Network Analysis

| Dataset Name | Description |
|---|---|
| `DEMO_GraphAnalysis` | Graph network dataset for path/community analysis |
| `DEMO_DIM` | Dimensional/graph data model dataset |

---

## 🏀 General / Benchmark / Fun

| Dataset Name | Description |
|---|---|
| `DEMO_BasketBall` | Basketball player/game statistics |
| `DEMO_TitanicSurvival` | Classic Titanic survival classification |
| `DEMO_HousingPrices` | Real estate price prediction |
| `DEMO_Car` | Automobile attributes and pricing |
| `DEMO_TPCH_1Gb` | TPC-H 1GB benchmark dataset (cloud only) |
| `DEMO_Plot` | Sample dataset for data visualization demos |
| `DEMO_Market` | Market/stock data |
| `DEMO_Email` | Email dataset for NLP/classification |
| `DEMO_ServiceNow` | ServiceNow IT service management data |

---

## 🔬 Solution Showcases (SolnShowCase_*)

These are pre-built end-to-end analytics showcases:

| Dataset Name | Description |
|---|---|
| `SolnShowCase_ChurnAnalytics` | Complete churn analytics solution |
| `SolnShowCase_JourneyAnalytics` | Customer journey analytics showcase |
| `SolnShowCase_ProductReco` | Product recommendation engine showcase |
| `SolnShowCase_Personalization` | Personalization engine (local only) |

---

## Notes

- Dataset names passed to `get_data()` must include the `_local` or `_cloud` suffix.
- Example: `CALL demo_user.get_data('DEMO_BankChurn_local');`
- The `_cloud` variant may not exist for all datasets — check `gs_tables_db.ddl` for exact names.
- GreenManufacturing has additional `_doug_` test variants that are internal/experimental.
