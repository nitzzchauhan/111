# Video Presentation Script: Feast Feature Store Integration
**Roll Number:** `22f2001251` (Nitin Chauhan)  
**Course:** MLOps — IIT Madras BS Degree | Week 3 Assignment  
**Topic:** Integrating Feast Feature Store into the IRIS Pipeline  

---

### A. Explaining the Problem Statement
> *"Hello everyone, I am Nitin Chauhan, roll number `22f2001251`. In this Week 3 assignment, our objective is to solve the training-serving skew problem in our Iris ML pipeline by integrating an open-source feature store: Feast. We need a unified system that handles historical point-in-time feature extraction for offline training and low-latency feature lookup for real-time inference without feature drift."*

---

### B. Explaining Your Approach to Reach the Objective
> *"My approach is broken into five core steps:*
> 1. *Structure a Feast repository with entities, data sources, and feature views.*
> 2. *Apply definitions to the central metadata registry (`registry.db`).*
> 3. *Materialize historical features into an online key-value store (`online_store.db`).*
> 4. *Refactor the training pipeline to fetch historical features via `get_historical_features()`.*
> 5. *Implement real-time inference using `get_online_features()` and validate zero training-serving skew."*

---

### C. Explaining and Demonstrating Cloud Compute Setup
> *"Here in the Google Cloud Console, I am using:*
> - *GCP Project: `project-97a8c7d5-b469-40bc-80c`*
> - *Compute Environment: GCP Vertex AI Workbench (`instance-20261011-192557`) in `us-central1-a` on an `e2-standard-4` machine (4 vCPUs, 16 GB RAM) running Debian 12.*
> - *Cloud Storage: `gs://mlops-assignment-iitm/week_3` for pipeline artifacts."*

---

### D. Explaining Input Files / Data
> *"The input dataset is the Iris flower dataset with four continuous features: `sepal_length`, `sepal_width`, `petal_length`, and `petal_width`.*
> - *`iris_features.parquet`: Full 150-sample dataset augmented with an entity key (`iris_id`) and UTC timestamps (`event_timestamp`, `created_timestamp`).*
> - *`iris_data_adapted_for_feast.csv`: Official adapted 45-sample time-series dataset."*

---

### E. Sequence of Actions Performed
> *"The sequence of execution steps is:*
> 1. *Opened terminal / SSH session in GCP Vertex AI Workbench.*
> 2. *Activated Python virtual environment and checked out Git branch `week_3`.*
> 3. *Ran `src/prepare_features.py` to prepare parquet sources.*
> 4. *Executed `feast apply` to register entities and views.*
> 5. *Executed `feast materialize` to load features into SQLite online store.*
> 6. *Ran `src/train.py` for model training and `src/inference.py` for online prediction."*

---

### F. Explanation of Scripts / Code and Objectives
> *"The codebase in `22f2001251_MLOPS_WEEKLY_ASSIGNMENT` contains:*
> - *`feature_store/feature_store.yaml`: Configures project name, local registry, and SQLite online store.*
> - *`feature_store/features.py`: Defines the `iris_id` Entity, Parquet `FileSource`, and `iris_features_view` with 365-day TTL.*
> - *`src/train.py`: Decouples training from raw CSV by using `store.get_historical_features()`, training a Decision Tree classifier.*
> - *`src/inference.py`: Queries `store.get_online_features()` with entity IDs and checks predictions.*
> - *`src/bigquery_store.py`: Documents enterprise architecture migration to GCP BigQuery.*
> - *`run_pipeline.py`: Single wrapper orchestrating the complete pipeline."*

---

### G. Errors Encountered & How They Were Overcome
> *"Two key challenges encountered:*
> 1. *Static Dataset Timestamps: Iris is static and lacks time fields. Solution: Synthesized realistic UTC timestamps in `prepare_features.py` ensuring Feast point-in-time joins work correctly.*
> 2. *Materialization Range: Initial materialization yielded empty records due to strict TTL window. Solution: Explicitly aligned the start and end UTC timestamps during `feast materialize`."*

---

### H. Working Demonstration of Pipeline in GCP Environment
> *(Action: Run `python run_pipeline.py` in terminal)*
> *"Now running `python run_pipeline.py`:*
> - *Step 1: Parquet datasets generated.*
> - *Step 2: Feast schema applied.*
> - *Step 3: 600 records materialized into SQLite.*
> - *Step 4: Training completed with 98.1% train accuracy and 93.3% test accuracy.*
> - *Step 5: Online inference completed — Zero training-serving skew validated (0.0% drift)."*

---

### I. Explaining Output Files / Data
> *"The generated pipeline outputs are:*
> - *`feature_store/data/registry.db` & `online_store.db`: Feast metadata and online store tables.*
> - *`models/iris_model.joblib`: Trained Decision Tree model.*
> - *`outputs/metrics.json`: Test accuracy, precision, recall, and F1 scores.*
> - *`outputs/inference_results.json`: Real-time predictions and 0.0% skew verification report.*
> - *`outputs/bigquery_tradeoffs.json`: Local vs BigQuery latency and cost comparison."*

---

### J. Learnings from this Assignment
> *"Three major takeaways:*
> 1. *Feast provides a single source of truth, completely eliminating training-serving skew.*
> 2. *Point-in-time joins prevent future data leakage in ML datasets.*
> 3. *Feature store architecture decouples feature engineering from model consumption, making features reusable across multiple teams and models."*
