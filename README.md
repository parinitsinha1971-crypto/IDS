# IDS
This project is a Machine Learning–based Intrusion Detection System (IDS) designed to detect SQL injection attempts in user-submitted text inputs.  
It uses a **hybrid feature pipeline** (TF-IDF + handcrafted features) and an **XGBoost classifier** to classify queries as *malicious* or *benign*.

## Features
- Detects classical, obfuscated, and tool-generated SQL injection payloads  
- Uses character-level TF-IDF (3–6 grams) for deep text pattern coverage  
- Adds hand-engineered features (entropy, keyword counts, special-char ratios, etc.)  
- XGBoost model with class-imbalance handling  
- Interactive CLI to test queries in real time

  ## Dataset
- Input column: `Sentence` (renamed to `query`)
- Label column: `Label` (binary: 0 = normal, 1 = malicious)
- Invalid rows removed and labels converted to integers

## Feature Engineering
1. **Character-level TF-IDF** (ngram 3–6, max 5000 features, fitted only on malicious samples)  
2. **Handcrafted features including:**
   - Query length  
   - Digit ratio  
   - Special character ratio  
   - Uppercase ratio  
   - Presence of semicolon  
   - Presence of SQL comments (`--`, `#`, `/*`)  
   - Quote count  
   - SQL keyword frequency  
   - Tool keyword frequency (e.g., sqlmap, nmap, metasploit, hydra)  
   - Shannon entropy  

These are combined into a single sparse feature matrix for the classifier.

## Model Used
### **XGBoost (XGBClassifier)**
Parameters:
- `n_estimators = 600`
- `max_depth = 10`
- `learning_rate = 0.05`
- `scale_pos_weight = auto-computed for class imbalance`
- `eval_metric = logloss`

The model is saved as:  
`sql_search_detector.pkl`

## Installation
1. Clone the repo  
2. Install dependencies:  
   `pip install -r requirements.txt`  
3. Run the detection script / notebook

## Project Structure
- Machine learning training code  
- TF-IDF vectorizer  
- Custom feature extractor  
- XGBoost classifier  
- Prediction wrapper function  
- Interactive CLI loop for live testing  

## Tech Stack
- Python 3  
- Scikit-learn  
- XGBoost  
- SciPy (sparse matrices)  
- pandas, numpy  
- Google Colab environment  

## Author
Parinit Sinha
