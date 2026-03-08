# Team Task Assignment

**Project:** Hidden Markov Models for Human Activity Recognition  
**Course:** Machine Learning Techniques II — Formative 2  
**Team:** Team 23, Cohort 2

---

## Team Members & Responsibilities

| Team Member | Role / Responsibility | Email | Device Configuration |
|-------------|----------------------|-------|---------------------|
| **Edith Githinji** | Data Collection & Model Implementation | e.githinji1@alustudent.com | iPhone 13 @ 100 Hz |
| **Liliane Gikundiro** | Data Collection & Feature Engineering | l.gikundiro@alustudent.com | iPhone 15 Pro Max @ 100 Hz |

---

## Task Breakdown

### Phase 1: Data Collection ✅
**Assigned to:** Both team members  
**Duration:** Week 1-2  
**Status:** Complete

- [x] Collect accelerometer + gyroscope data for 4 activities (still, standing, walking, jumping)
- [x] Ensure consistent 100 Hz sampling rate across both devices
- [x] Record at least 12 samples per activity
- [x] Organize data into folder structure: `activity_number/Accelerometer.csv` + `Gyroscope.csv`
- [x] Verify timestamp alignment between accelerometer and gyroscope streams

---

### Phase 2: Data Preprocessing & Visualization ✅
**Assigned to:** Edith Githinji  
**Duration:** Week 2-3  
**Status:** Complete

- [x] Implement `load_recording()` function for CSV parsing
- [x] Merge accelerometer and gyroscope data using `pd.merge_asof()`
- [x] Create 80/20 stratified train/test split
- [x] Generate raw signal visualizations (Figure 1)
- [x] Verify data quality (check for missing values, outliers)

---

### Phase 3: Feature Extraction ✅
**Assigned to:** Liliane Gikundiro  
**Duration:** Week 3-4  
**Status:** Complete

- [x] Design 7 time-frequency domain features
- [x] Implement sliding window approach (50 samples, 25-sample step)
- [x] Extract features: `acc_rms`, `acc_var`, `sma`, `gyro_rms`, `corr_xy`, `dom_freq`, `spec_energy`
- [x] Apply Z-score normalization using `StandardScaler`
- [x] Generate feature distribution plots (Figure 2)

---

### Phase 4: HMM Implementation ✅
**Assigned to:** Both team members (pair programming)  
**Duration:** Week 4-6  
**Status:** Complete

- [x] Implement `GaussianHMM` class from scratch
- [x] Forward-backward algorithm (log-space for stability)
- [x] Baum-Welch EM training loop
- [x] Viterbi decoding with backpointer matrix
- [x] Parameter initialization strategy
- [x] Convergence monitoring (log-likelihood)

---

### Phase 5: Model Training & Classification ✅
**Assigned to:** Edith Githinji  
**Duration:** Week 6-7  
**Status:** Complete

- [x] Train 4 separate 1-state HMMs (one per activity)
- [x] Implement maximum likelihood window classification
- [x] Train joint 4-state HMM for sequence decoding
- [x] State-to-activity alignment using mean distance matching
- [x] Generate convergence plots (Figure 3)

---

### Phase 6: Evaluation & Visualization ✅
**Assigned to:** Liliane Gikundiro  
**Duration:** Week 7-8  
**Status:** Complete

- [x] Compute classification accuracy on train/test sets
- [x] Generate confusion matrix (Figure 7)
- [x] Visualize transition matrix heatmap (Figure 4)
- [x] Plot emission parameters (Figure 5)
- [x] Create Viterbi decoded sequence plots (Figure 6)
- [x] Feature importance analysis (Figure 8)

---

### Phase 7: Documentation & Submission ✅
**Assigned to:** Both team members  
**Duration:** Week 8  
**Status:** Complete

- [x] Write comprehensive README.md
- [x] Document code with docstrings and comments
- [x] Organize repository structure
- [x] Create presentation slides (if required)
- [x] Final notebook review and cleanup
- [x] Submit assignment via GitHub

---

## Collaboration Tools

- **Version Control:** Git + GitHub  
- **Repository:** https://github.com/Edith123321/markov_models
- **Primary Branch:** `main`
- **Feature Branch:** `featurextraction` (merged)
- **Communication:** WhatsApp + Email

---

## Deliverables Checklist

- [x] `hidden_markov.ipynb` — Complete analysis notebook
- [x] `data/` — Sensor recordings (52 activity folders)
- [x] `figures/` — 8 publication-quality visualizations
- [x] `README.md` — Project documentation
- [x] `TASKS.md` — Task assignment tracker (this file)
- [x] Git commit history showing contribution from both members

---

## Notes & Decisions

### Design Choices
1. **1-state per activity:** Simplifies training and provides baseline classifier
2. **Diagonal covariance:** Assumes feature independence, reduces parameters
3. **Joint 4-state HMM:** Enables Viterbi sequence-level decoding
4. **Z-score normalization:** Required for Gaussian emission assumptions
5. **Window size 0.5s:** Balances temporal resolution vs. sufficient samples for FFT

### Challenges Overcome
- **Timestamp alignment:** Used `pd.merge_asof()` with 5ms tolerance
- **Merge conflicts:** Resolved via `git checkout --ours` strategy during feature branch integration
- **Numerical stability:** Implemented log-space forward-backward to prevent underflow
- **State alignment:** Automatic state-to-activity mapping using centroid distance

---

## Timeline Summary

| Week | Milestone | Status |
|------|-----------|--------|
| 1-2 | Data collection complete | ✅ |
| 3-4 | Feature extraction implemented | ✅ |
| 5-6 | HMM class fully functional | ✅ |
| 7 | Training & classification complete | ✅ |
| 8 | Documentation & submission | ✅ |

---

**Last Updated:** March 8, 2026  
**Project Status:** Complete ✅
