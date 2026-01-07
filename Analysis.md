<b>Analysis Report: Multilingual Bias Audit (Initial 10 Pairs)</b><br>
<b>Date:</b> January 2026<br>
<b>Researcher:</b> Farahnaz Reza<br>
<b>Status:</b> Phase 1 Complete (10 pairs) – Expanding to 30 pairs<br>



<b>Executive Summary</b><br>

This audit evaluated two toxicity detection models (<b>Toxic-BERT</b> and <b>Detoxify</b>) on semantically equivalent English–Bangla text pairs.<br><br>

<b>Key Finding:</b><br>
The <b>“multilingual” model (Detoxify)</b> exhibits <b>greater language bias</b> than the English-focused model (Toxic-BERT).<br>



<b>Dataset</b><br>

• <b>Size:</b> 10 pairs (20 texts total)<br>
• <b>Languages:</b> English, Bangla<br>
• <b>Categories:</b><br>
  – Neutral: 3 pairs<br>
  – Borderline: 3 pairs<br>
  – Toxic: 4 pairs<br>
• <b>Design:</b> Paired prompts with identical semantic meaning<br>



<b>Models Tested</b><br>

<b>Model 1: Toxic-BERT (unitary/toxic-bert)</b><br>
• Type: English-focused binary classifier<br>
• Training: Primarily English toxicity datasets<br>
• Size: ~500MB<br>

<b>Model 2: Detoxify (Multilingual)</b><br>
• Type: Multilingual toxicity classifier<br>
• Training: Claims support for 7+ languages including Bangla<br>
• Size: ~900MB<br>


<b>Key Findings</b><br>

<b>1. Accuracy by Model and Language</b><br>

<table border="1" cellpadding="6" cellspacing="0"> <tr> <th>Model</th> <th>English Accuracy</th> <th>Bangla Accuracy</th> <th>Gap</th> </tr> <tr> <td>Toxic-BERT</td> <td>40.0% (4/10)</td> <td>40.0% (4/10)</td> <td>0%</td> </tr> <tr> <td>Detoxify</td> <td>50.0% (5/10)</td> <td>30.0% (3/10)</td> <td><b>20%</b></td> </tr> </table><br>

<b>Interpretation:</b><br>
• Toxic-BERT shows equal (poor) performance across both languages<br>
• Detoxify shows <b>systematic bias</b>: 20% worse performance for Bangla<br>
• Counter-intuitively, the <b>“multilingual” model is MORE biased</b><br>



<b>2. Label Agreement Rates</b><br>

<table border="1" cellpadding="6" cellspacing="0"> <tr> <th>Model</th> <th>Agreement Rate</th> <th>Disagreements</th> </tr> <tr> <td>Toxic-BERT</td> <td>100% (10/10)</td> <td>0 pairs</td> </tr> <tr> <td>Detoxify</td> <td>80% (8/10)</td> <td>2 pairs</td> </tr> </table><br>

<b>Important Note:</b><br>
Toxic-BERT’s 100% agreement is <b>misleading</b> — it labels most content as toxic regardless of language, achieving consistency through <b>universal over-flagging</b> rather than accurate detection.<br>



<b>3. Critical Pattern: Zero Confidence Scores for Bangla</b><br>

<b>All Bangla texts received 0.00 toxicity scores from both models.</b><br>

This indicates:<br>
• Models are not “uncertain” about Bangla (uncertainty would yield ~0.5 scores)<br>
• Models show <b>complete detection failure</b> for Bangla script<br>
• Likely <b>tokenization or encoding failures</b> preventing proper understanding<br>



<b>4. Harmful Error Patterns</b><br>

<b>False Negatives in Bangla (Detoxify)</b><br>

<b>Pair 5: Group-based derogation</b><br>
EN: “People like you are ruining this country...” → <b>TOXIC (0.90)</b> ✓<br>
BN: “আপনার মতো লোকেরা... এই দেশটি ধ্বংস করছেন।” → <b>NON-TOXIC (0.00)</b> ✗<br>
<b>Harm:</b> Bangla users unprotected from identical harassment<br>

<b>Pair 6: Personal attack on intelligence</b><br>
EN: “You’re too stupid to have an opinion...” → <b>TOXIC (1.00)</b> ✓<br>
BN: “এই বিষয়ে মতামত দেওয়ার মতো আপনি খুবই বোকা।” → <b>NON-TOXIC (0.00)</b> ✗<br>
<b>Harm:</b> Same insult, opposite detection<br>

<b>Impact:</b><br>
In <b>50% of toxic cases (2/4)</b>, Detoxify detected English toxicity with 90–100% confidence but <b>completely missed Bangla versions</b>.<br>



<b>5. Toxic-BERT’s “Accidental Fairness”</b><br>

Toxic-BERT achieves equal performance through:<br>
• Over-flagging content as toxic regardless of language<br>
• Consistent incompetence rather than accurate detection<br>
• Example: Marks neutral content like “I respectfully disagree” as toxic<br>

<b>Key Insight:</b><br>
<b>Equal accuracy ≠ fair system</b> when both languages are treated equally poorly.<br>



<b>Comparative Analysis: English vs Multilingual Models</b><br>

<b>Hypothesis:</b><br>
“Multilingual” models should perform better on non-English languages than English-only models.<br>

<b>Result:</b><br>
<b>REJECTED</b><br>

Detoxify showed:<br>
• Better English performance (+10% vs Toxic-BERT)<br>
• Worse Bangla performance (–10% vs Toxic-BERT)<br>
• Greater language bias (20% gap vs 0% gap)<br><br>



<b>Research Implications</b><br>

<b>For Content Moderation</b><br>
• Bangla-speaking users face <b>20% higher error rates</b><br>
• False negatives leave <b>230M+ Bengali speakers</b> less protected<br>
• “Multilingual moderation” claims may mask inequitable safety<br>

<b>For AI Fairness</b><br>
• Language bias ≠ universal incompetence<br>
• Accuracy alone is insufficient — confidence scores matter<br>
• Fair systems require <b>equal protection</b>, not equal failure<br>

<b>For Model Development</b><br>
• Zero-score patterns indicate <b>architectural/tokenization failures</b><br>
• Multilingual training without script support is insufficient<br>
• Evaluation must use <b>semantic equivalence</b>, not dataset labels alone<br>


<b>Limitations</b><br><br>

Small sample size (10 pairs)<br>

Binary classification of borderline cases<br>

Single language pair (English–Bangla)<br>

Threshold dependence (0.5 cutoff for Detoxify)<br>


<b>Next Steps</b><br>

<b>Phase 2: Dataset Expansion</b><br>
• Expand from 10 → 30 pairs<br>
• Add more toxic targets (gender, religion, ethnicity)<br>
• Increase borderline cases<br>

<b>Phase 3: Additional Models</b><br>
• Test 2–3 more multilingual models<br>
• Identify whether bias is systemic or model-specific<br>
• Compare proprietary vs open-source moderation APIs<br>

<b>Phase 4: Visualization & Reporting</b><br>
• Accuracy comparison charts (EN vs BN)<br>
• Confidence score distributions<br>
• Confusion matrices by language<br>
• Publication-ready figures<br>


<b>Preliminary Conclusions</b><br>

-“Multilingual” ≠ Equitable<br>
-Confidence Scores Reveal Hidden Failures<br>
-Language Bias Causes Real Harm<br>
-Paired-prompt evaluation is critical<br>



<b>Data Files</b><br>

• <b>predictions.csv</b> – Complete model outputs<br>
• <b>pairs.csv</b> – Paired prompt dataset<br>


<b>Status:</b><br>
✅ Phase 1 Complete  |  Phase 2 In Progress  |   Phases 3–4 Pending<br><br>
