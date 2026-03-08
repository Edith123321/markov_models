# Hidden Markov Models for Human Activity Recognition

**Formative 2 — Group Assignment**  
**Course:** Machine Learning Techniques II  
**Team 23 — Cohort 2**

## Team Members

| Name | Role/Responsibility | Email | Device |
|------|---------------------|-------|--------|
| **Edith Githinji** | Data Collection & Implementation | e.githinji1@alustudent.com | iPhone 13 @ 100 Hz |
| **Liliane Gikundiro** | Data Collection & Implementation | l.gikundiro@alustudent.com | iPhone 15 Pro Max @ 100 Hz |

---

## Project Overview

This project implements Hidden Markov Models (HMMs) to classify human activities from smartphone sensor data. Using accelerometer and gyroscope measurements collected at 100 Hz, we train Gaussian HMMs to recognize four distinct activities:

- **Still** — Stationary with minimal movement
- **Standing** — Stationary but upright  
- **Walking** — Normal gait locomotion
- **Jumping** — Vertical dynamic motion

---

## Technical Approach

### Data Collection
- **Devices:** iPhone 13 and iPhone 15 Pro Max
- **Sampling Rate:** 100 Hz (harmonized between devices)
- **Sensors:** 3-axis accelerometer + 3-axis gyroscope
- **Recording Structure:** Separate folders per activity with `Accelerometer.csv` and `Gyroscope.csv`

### Feature Engineering
We extract **7 features** per 0.5-second window (50 samples @ 100 Hz):

| Feature | Domain | Description |
|---------|--------|-------------|
| `acc_rms` | Time | Overall motion intensity |
| `acc_var` | Time | Variance of acceleration magnitude |
| `sma` | Time | Signal Magnitude Area (energy proxy) |
| `gyro_rms` | Time | Rotation magnitude |
| `corr_xy` | Time | X-Y acceleration correlation |
| `dom_freq` | Frequency | Dominant FFT frequency |
| `spec_energy` | Frequency | Energy in 0.5–4 Hz locomotion band |

**Normalization:** Z-score standardization (fit on training set)

### Model Architecture
- **Baseline:** 4 separate 1-state Gaussian HMMs (one per activity)
- **Advanced:** 4-state joint HMM with Viterbi decoding for sequence classification
- **Training:** Baum-Welch EM algorithm
- **Decoding:** Forward-backward algorithm + Viterbi path

---

## Repository Structure

```
markov_models/
├── hidden_markov.ipynb          # Main analysis notebook
├── TASKS.md                      # Task assignment spreadsheet
├── README.md                     # This file
├── data/                         # Raw sensor recordings
│   ├── Metadata.csv
│   ├── jumping_1/
│   │   ├── Accelerometer.csv
│   │   └── Gyroscope.csv
│   ├── standing_1/
│   ├── still_1/
│   ├── walking_1/
│   └── ...
└── figures/                      # Generated visualizations
    ├── fig1_raw_signals.png
    ├── fig2_feature_distributions.png
    ├── fig3_convergence.png
    ├── fig4_transition_matrix.png
    ├── fig5_emission_params.png
    ├── fig6_viterbi_decoded.png
    ├── fig7_confusion_matrix.png
    └── fig8_feature_importance.png
```

---

## Getting Started

### Prerequisites
```bash
pip install numpy pandas matplotlib seaborn scipy scikit-learn jupyter
```

### Running the Analysis
1. **Clone the repository:**
   ```bash
   git clone https://github.com/Edith123321/markov_models.git
   cd markov_models
   ```

2. **Ensure data directory exists:**
   ```bash
   # Verify ./data folder contains activity folders
   ls data/
   ```

3. **Run the notebook:**
   ```bash
   jupyter notebook hidden_markov.ipynb
   ```
   Or open in VS Code with Jupyter extension.

4. **Execute cells sequentially** (cells must run in order for proper initialization)

---

## Key Results

- **Train/Test Split:** 80/20 stratified by activity
- **Window-based Classification:** Achieves high accuracy distinguishing dynamic (jumping/walking) from static (still/standing) activities
- **Viterbi Decoding:** Provides temporally coherent activity sequences by leveraging state transition structure
- **Feature Importance:** Dominant frequency and spectral energy are most discriminative for classifying locomotion patterns

---

## Implementation Highlights

### Custom Gaussian HMM Class
We implement a full Gaussian HMM from scratch with:
- **Forward-backward algorithm** in log-space (numerical stability)
- **Viterbi decoding** with backpointer matrix
- **Baum-Welch EM training** with convergence monitoring
- **Diagonal covariance structure** (independence assumption)

### Classification Strategy
1. **Per-activity HMMs:** Train separate 1-state model for each activity
2. **Maximum likelihood classification:** Assign window to activity with highest log-likelihood
3. **Viterbi decoding:** Use joint 4-state HMM to decode entire sequences, smoothing noisy frame-level predictions

---

## Visualizations

The notebook generates 8 publication-quality figures:
1. Raw accelerometer + gyroscope signals per activity
2. Z-scored feature distributions per activity
3. Training convergence (log-likelihood vs. iteration)
4. Learned transition matrix heatmap
5. Emission parameter means (μ) per state
6. Viterbi decoded activity sequences
7. Confusion matrix (test set predictions)
8. Feature importance analysis

---

## References

- **Baum-Welch Algorithm:** Baum et al. (1970) "A Maximization Technique Occurring in the Statistical Analysis of Probabilistic Functions of Markov Chains"
- **Viterbi Algorithm:** Viterbi (1967) "Error Bounds for Convolutional Codes"
- **Activity Recognition Survey:** Lara & Labrador (2013) "A Survey on Human Activity Recognition using Wearable Sensors"

---

## License

This project is developed for educational purposes as part of the Machine Learning Techniques II course at ALU.

---

## Contact

For questions or collaboration, please contact:
- **Edith Githinji:** e.githinji1@alustudent.com
- **Liliane Gikundiro:** l.gikundiro@alustudent.com

**Repository:** https://github.com/Edith123321/markov_models
