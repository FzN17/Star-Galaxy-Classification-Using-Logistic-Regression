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
+---------------------------+       +----------------------------+       +-----------------------------+
|   Data Inspection &       |       |  Data Partitioning         |       |   Baseline Modeling         |
|   Feature Engineering     | ----> |  - 70% Train Set           | ----> |   - Logistic Regression     |
|   - 2,000 SDSS Objects    |       |  - 30% Test Set            |       |   - High Interpretability   |
+---------------------------+       +----------------------------+       +-----------------------------+
                                                                                        |
                                                                                        v
+---------------------------+       +----------------------------+       +-----------------------------+
|   Feature Importance      |       |  Multi-Metric Evaluation   |       |   Generalization Check      |
|   - Coefficient Analysis  | <---- |  - Precision/Recall (97%)  | <---- |   - 5-Fold Cross Validation |
|   - Sign/Magnitude Check  |       |  - ROC-AUC Curve (0.996)   |       |   - Stable Std Dev (0.017)  |
+---------------------------+       +----------------------------+       +-----------------------------+
