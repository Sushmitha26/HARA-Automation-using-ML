# HARA Automation

## Goal  
Automate key parts of the ISO 26262 HARA process for an EV powertrain by predicting hazardous events and their ASIL risk.

---

## Project Overview  
HARA (Hazard Analysis and Risk Assessment) is a systematic process for identifying hazards due to malfunctioning items or functions (e.g. brake system, powertrain, drive-assist) and evaluating their risks. It’s widely used in safety-critical industries (Automotive, Aerospace, Machinery, Nuclear, Medical Device, etc.).

1. **Hazardous-Event Prediction**  
   - Combine each Operating Scenario with each potential Hazard to predict one of six events (or “no event”):  
     1. Collision with pedestrians  
     2. Collision with cyclists  
     3. Electric shock  
     4. Front-end collisions  
     5. Side collisions  
     6. Rear-end collisions  

2. **ASIL Risk Evaluation**  
   - Predict:  
     - **Severity** of the hazardous event (S0–S3)  
     - **Controllability** by traffic participants (C0–C3)  
     - **People at risk**  
   - Parse or regress **Δv** (impact velocity)  
   - Combine predicted S, C, and given Exposure (E1–E4) via an ISO 26262 lookup table to assign an **ASIL** (QM, A–D).

---

## Features  
- **Text → Embeddings:**  
  Use HuggingFace’s SentenceTransformer (`all-MiniLM-L6-v2`) to encode scenario+hazard text.  
- **Multi-class Models:**  
  - **Hazardous Event, Severity & Controllability, People at Risk:**  
    RandomForestClassifier & LogisticRegression  
  - **Δv Regression:**  
    RandomForestRegressor (embeddings + [E, S, C])  
- **ASIL Lookup:**  
  ISO 26262 table to compute ASIL from S, E, C  
- **Template-Based Rationales:**  
  Auto-generate human-readable severity & controllability explanations.  
- **End-to-End Pipeline:**  
  1. Excel → scenario–hazard pairs  
  2. Model training & test  
  3. Excel → final predictions & rationales

---

## Dependencies  
- **Python:** 3.8+  
- **Libraries:**  
  - pandas  
  - numpy  
  - scikit-learn  
  - sentence-transformers  
  - openpyxl

---

## Evaluation
Classification report & accuracy for each task
MSE & R² for Δv regression
