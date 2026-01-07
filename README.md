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
    └── project_report.pdf     # Full write-up\
<br>
7. **Key Findings**
Key Findings (Phase 1: 10 Pairs)\
<b>Counter-Intuitive Discovery:</b> “Multilingual” Models Show GREATER Bias<br><br>

<b>Model</b> | <b>English Accuracy</b> | <b>Bangla Accuracy</b> | <b>Bias Gap</b><br>
Toxic-BERT (English-focused) | 40% | 40% | 0%<br>
Detoxify (Multilingual) | 50% | 30% | <b>20%</b><br>

<b>The “multilingual” model performed 20% worse on Bangla despite claiming language support.</b><br>
<b>Critical Pattern:</b> Complete Detection Failure<br>

• <b>All Bangla texts scored 0.00</b> (indicating total failure, not low confidence)<br>
• <b>2 out of 4 toxic Bangla texts</b> completely missed by Detoxify<br>
• Same insults detected with <b>90–100% confidence in English</b>, <b>0% in Bangla</b><br>

<b>Example:</b>\
EN: “You’re too stupid to have an opinion” → <b>Detoxify: TOXIC (1.00)</b><br>
BN: “আপনি খুবই বোকা” (identical meaning) → <b>Detoxify: NON-TOXIC (0.00)</b><br>

<b>Implication:</b><br>
Bangla users face <b>identical harassment</b> but receive <b>less protection</b>.<br>



<b> Methodology</b><br>
<b>Paired Prompts Design</b><br>
<b>30 semantically equivalent text pairs (English/Bangla)</b><br>
  – 10 complete<br>
  – 20 in progress<br>

<b>Prompt Categories</b><br>
-<b>Neutral (10 pairs):</b> Baseline to test false positives<br>
-<b>Borderline (10 pairs):</b> Ambiguous cases<br>
-<b>Toxic (10 pairs):</b> Clear harassment and hate speech<br><br>

-Each Bangla text is <b>naturally phrased</b>, not word-for-word translated<br>
-<b>Intent controlled</b> to isolate language as the variable<br><br>

<b>Models Tested</b><br>

-<b>Toxic-BERT</b> (unitary/toxic-bert)<br>
  – English-focused toxicity detector (~500MB)<br>
<b>Detoxify (Multilingual)</b><br>
  – Claims support for 7+ languages including Bangla (~900MB)<br>
-<b>Future:</b> Testing 2–3 additional multilingual models (Phase 3)<br>

<b>Evaluation Metrics</b><br>

-<b>Accuracy by Language</b><br>
-<b>Label Agreement Rate</b><br>
-<b>Confidence Score Analysis</b> (0.00 patterns)<br>
-<b>Harmful Error Patterns</b><br>
  – False negatives in Bangla<br>
  – False positives in Bangla<br>
-<b>Qualitative Analysis</b><br>


<b>Current Results Summary</b><br>
<b>Phase 1 Analysis</b> (10 pairs / 20 texts)<br>

<b>Completed:</b><br>
-Dataset collected and validated<br>
-Both models evaluated<br>
-Bias patterns documented<br>
-Results saved to <b>results/predictions.csv</b><br><br>

<b>Key Statistics:</b><br>

-<b>False negatives (Bangla):</b> 2/4 toxic cases missed by Detoxify<br>
-<b>Label agreement:</b><br>
  – Detoxify: 80%<br>
  – Toxic-BERT: 100% (misleading due to over-flagging)<br>
-<b>Confidence scores:</b><br>
  – 100% of Bangla texts scored <b>0.00</b><br>

<b>Major Finding:</b><br>
<b>Multilingual models can be MORE biased than monolingual ones</b>, challenging assumptions about “multilingual AI.”<br>
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
