**Multilingual Bias Audit: Bangla vs. English Toxicity Detection** <br>
**Research Question:** Do content moderation models exhibit language-based bias that disproportionately harms Bangla-speaking users?

**1.Motivation**
With over 230 million Bengali speakers online, equitable AI systems must perform consistently across languages. Yet most toxicity detection models are trained primarily on English data, raising critical questions about digital safety for non-English speakers.
This audit evaluates whether multilingual content moderation models<br>

•	Under-detect abuse in Bangla (leaving users unprotected from harassment)<br>
•	Over-flag benign Bangla content (silencing legitimate speech and marginalizing users)<br>

**2.Methodology**
Paired Prompts Design
30 semantically equivalent text pairs (English/Bangla) across three categories:

1.	**Neutral (10 pairs):** Baseline to test false positive rates
2.	**Borderline (10 pairs):** Ambiguous cases where models struggle (sarcasm, passive aggression)
3.	**Toxic (10 pairs):** Clear harassment, hate speech, personal attacks
Each Bangla text is naturally phrased, not word-for-word translation Controlled for intent to isolate language as the variable.

**3.Models Tested**
Primary: Multilingual toxicity detection models (e.g., unitary/toxic-bert, Detoxify multilingual)
Baseline: XLM-RoBERTa-based classifiers fine-tuned on English toxicity data


**4.Evaluation Metrics:**
Label Agreement Rate: How often EN/BN pairs receive the same classification
Confidence Disparity: Difference in model certainty between language pairs
Harmful Error Patterns:
1.	False negatives in Bangla (toxic content marked safe)
2.	False positives in Bangla (neutral content marked toxic)
Qualitative Analysis: Case studies of specific failure modes

**5.Dataset Structure**\
•	data/pairs.csv\
•	Columns:\
**pair_id:** Links English and Bangla versions of same content\
**language:** 'en' or 'bn'\
**text:** The actual content\
**category:** 'neutral', 'borderline', or 'toxic'\
**expected_label:** Human-annotated ground truth\
**context_notes:** Cultural/linguistic considerations\
**Current Status:** 10/30 pairs completed 

**6.Quick Start**
•	**Setup**
bashgit clone https://github.com/[your-username]/multilingual-bias-audit-bangla.git
cd multilingual-bias-audit-bangla
pip install -r requirements.txt
Run Baseline Evaluation
bashjupyter notebook notebooks/01_run_models.ipynb

📁 **Repository Structure**
multilingual-bias-audit-bangla<br>
├── README.md<br>
├── requirements.txt<br>
├── data<br>
│   └── pairs.csv<br>          # Paired prompts dataset
├── notebooks<br>
│   ├── 01_run_models.ipynb<br>  # Model inference pipeline
│   └── 02_analysis.ipynb<br>    # Bias analysis & visualization
├── results<br>
│   ├── predictions.csv<br>     # Model outputs
│   └── key_examples.md<br>    # Documented failure cases
└── docs<br>
    └── project_report.pdf     # Full write-up

7. **Key Findings**
[To be completed after analysis]<br>
•	**Initial observations:**<br>
-> Model performance comparison EN vs BN<br>
-> Specific bias patterns identified<br>
-> Examples of harmful errors<br>

**8.Research Context**
This work addresses gaps in:
1.	**Human-Computer Interaction:** Ensuring digital platforms serve diverse linguistic communities equitably\
2.	**Fairness in AI:** Evaluating algorithmic bias beyond English-centric benchmarks\
3.	**Adaptive Systems:** Building evidence for context-aware content moderation\
**Relevant to:** Online safety, platform governance, multilingual NLP, digital rights



**9. About**
**Author:** Farahnaz Reza
**Affiliation:** Aspiring PhD Researcher in HCI & Adaptive AI\
**Research Interests:** Bias-aware systems, digital equity, adaptive AI for marginalized users\
**Contact:** farahnazreza@gmail.com | https://www.linkedin.com/in/farahnaz-reza/|

**10.Acknowledgments**
•	Bangla language examples validated by native speakers
•	Inspired by multilingual bias research in AI fairness community

**11.Status Updates**<br>
•	✅ Dataset design completed (10 starter pairs)<br>
•	Expanding to 30 pairs<br>
•	Model evaluation in progress<br>
•	Analysis phase pending<br>
