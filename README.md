# Star-Galaxy-Classification-Using-Logistic-Regression
# Pillar 1: Problem Understanding (Context & Scope)
The cornerstone of any analytical workflow is a precise grasp of the core objective, its significance, and the constraints of the environment.
- **The Objective**: The primary task is to develop an automated binary classification model capable of distinguishing between two fundamental types of celestial objects—Stars (0) and Galaxies (1)—using photometric data extracted from the Sloan Digital Sky Survey (SDSS).
- **The Scientific Relevance**: Modern sky surveys capture billions of astronomical sources, making manual visual classification by astronomers impossible. Automated machine learning classification is critical to scaling up data processing pipelines, enabling large-scale cosmological studies, mapping the distribution of matter in the universe, and isolating clean stellar or galactic samples for target follow-ups.
- **The Boundary Conditions**: The problem must be solved using a minimalistic, highly interpretable framework. This requires selecting features that balance low measurement noise with high discriminant capacity, avoiding overly complex models unless simpler linear boundaries fail.

# Pillar 2: Research Skill (Domain Knowledge Integration)
Data without context is noise. Demonstrating research skill involves looking beneath the column headers to understand the physical and astronomical principles that govern the data attributes.
The dataset provides four features for 2,000 unique observations: `u_g`, `g_r`, `r_i`, and `petro_radius`. Researching SDSS standards reveals the physical meaning of these attributes:
- **Color Indices** (_u−g_,_g−r_,_r−i_): These features represent the difference in apparent magnitudes across consecutive optical filters (_u_=ultraviolet, _g_=green, _r_=red, _i_=near-infrared). In astronomy, a color index serves as a proxy for the spectral energy distribution (SED). It reflects parameters like an object's temperature, chemical composition, stellar age, and cosmological redshift (_z_).
- Petrosian Radius (`petro_radius`): This is a morphometric metric that measures the spatial distribution of light from an object, calculated independently of the object's distance or sky background brightness.
## Formulating Domain Hypotheses:
- **Morphological Hypothesis**: Stars are point-like light sources whose apparent profiles are entirely determined by atmospheric distortion (the Point Spread Function, or PSF). Conversely, galaxies are extended, resolved structures containing billions of stars. Therefore, galaxies should fundamentally exhibit a systematically larger `petro_radius` than stars.
- **Photometric Hypothesis**: Galaxies exhibit integrated light signatures from diverse stellar populations, dust extinction, and cosmological redshift, which typically pushes their color indices toward the redder spectrum (higher _g−r_ and _r−i_ values) compared to a typical main-sequence star in our galaxy.

# Pillar 3: Effective Problem Solving (Technical Workflow)
An effective problem-solving strategy translates domain hypotheses into an elegant, reliable, and rigorously validated machine learning architecture.
The implemented pipeline systematically executes this solution:
1. **Data Stratification & Splitting**: The 2,000 records are partitioned into a 70% training set (1,400 samples) and a 30% validation set (600 samples). This ensures that validation performance remains an unbiased estimator of true generalization.
2. **Algorithm Selection**: A Logistic Regression model is selected. While non-linear architectures (like Random Forests or Neural Networks) are powerful, starting with a generalized linear model helps test if the feature space is linearly separable, providing clean, mathematically derivable feature importances.
3. **Robust Validation Guardrails**: Rather than trusting a single train-test split, a 5-fold Cross-Validation (CV) routine is integrated. This iteratively evaluates the model on unseen subsets of the training data to confirm that the performance is not an artifact of data sorting.
4. **Multi-Dimensional Evaluation**: The model is evaluated beyond simple accuracy by utilizing a Confusion Matrix, a detailed Classification Report (Tracking Precision, Recall, and F1​-score for both classes), and a Receiver Operating Characteristic (ROC) curve to isolate the Area Under the Curve (AUC).

# Pillar 4: Good Logical Explanation (Synthesis & Interpretation)
The final stage bridges the gap between machine learning metrics and scientific reality, explaining why the model behaves the way it does and validating its logic against physical laws.
The evaluation yields the following results:
- Training Accuracy: 0.964 (96.4%)
- Test Accuracy: 0.972 (97.2%)
- 5-Fold CV Accuracy: 0.964±0.017
- ROC-AUC Score: 0.996
