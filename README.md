# twitter_sentiment_project
twitter_sentiment_project
Customer Sentiment on Twitter: Executive AI Analysis


Prepared for: Armin Kajevic, Senior Management Consultant
Format: Google Colab-ready notebook, reproducible source code, executive evidence pack, and presentation materials

Executive Summary

This repository demonstrates a decision-oriented workflow for analysing customer-support conversations on Twitter. It combines Gemini for rapid dataset orientation, AutoViz for automated exploratory visualisation, and a Twitter-specialised Hugging Face RoBERTa model for sentiment classification. The objective is not merely to generate charts or labels. It is to show how AI can accelerate discovery while preserving the human interpretation needed for trustworthy management decisions.

The supplied sample.csv was processed end to end. It contains 93 tweets, including 49 inbound customer tweets. The Twitter-specific sentiment model classified 26 inbound tweets as negative (53.1%), 18 as neutral (36.7%), and 5 as positive (10.2%). These values are sample-specific and must not be presented as a benchmark for the full corpus or for any brand.

Deliverable
Purpose
Location
Colab notebook
One-click, documented workflow ready to upload/run in Google Colab
notebooks/customer_sentiment_twitter_executive.ipynb
Reproducible analysis script
Local or cloud analysis with curated charts and tables
src/run_analysis.py
AutoViz script
Automated EDA on business-interpretable features
src/run_autoviz.py
Validation script
Low-confidence queue and human-review template without false accuracy claims
src/build_validation_pack.py
Executive insight memo
Evidence-led interpretation and management recommendations
docs/executive_insights.md
Model validation note
Transparency on confidence, sarcasm, and absence of ground truth
docs/model_validation.md
Presentation outline
Executive narrative for the accompanying presentation
presentation/slide_content.md




Start in Google Colab

Open notebooks/customer_sentiment_twitter_executive.ipynb in Google Colab after pushing this repository to GitHub. Use the notebook’s upload cell to select either the supplied sample.csv or the full twcs.csv file. For the full Customer Support on Twitter corpus, download the file from Kaggle and do not commit it to the repository. The dataset has its own provenance and licensing terms .

The notebook installs compatible dependencies, runs a data-quality profile, creates curated visualisations, runs AutoViz, and scores inbound customer tweets using cardiffnlp/twitter-roberta-base-sentiment-latest. For large datasets, it applies a deterministic hash-based sample before resource-intensive visualisation and inference. This preserves reproducibility and prevents accidental exhaustion of a standard Colab runtime.

Step
Action in Colab
Expected output
1
Run Setup
Pinned, compatible libraries are installed.
2
Upload twcs.csv or sample.csv
File path is validated and dataset mode is reported.
3
Run Dataset Profile
Schema, data types, missingness, timeframe, and directionality.
4
Add GEMINI_API_KEY in Colab Secrets and run Gemini Exploration
AI-generated schema and analytical-priority narrative.
5
Run AutoViz
Automated EDA images saved under autoviz_outputs/.
6
Run Sentiment Analysis
Negative, neutral, and positive labels for inbound customer tweets.
7
Run Validation & Export
Human-review queue, curated charts, CSVs, and a downloadable ZIP.




Optional Gemini Setup

The Gemini step is optional and intentionally skips safely if no key is supplied. In Colab, add a secret named GEMINI_API_KEY in the left-side Secrets panel, enable notebook access, and rerun the Gemini cell. The notebook uses Google’s current google-genai SDK pattern . Never hard-code an API key or commit it to GitHub.

The Gemini prompt receives only a compact metadata profile and a small, redacted data preview. It should not be sent sensitive, personal, or confidential data without appropriate approval. Gemini’s output is treated as an exploratory aid, not as an authoritative finding.

Why These Tools

Tool
Role in the workflow
What it accelerates
What it cannot decide
Gemini
Initial dataset orientation
Schema narration, missingness review, and analytical hypotheses
Statistical validity, causality, or business priorities
AutoViz
Automated exploratory data analysis
Fast scan of distributions and potential relationships
Which charts matter to decision-makers or whether patterns are material
Twitter-RoBERTa
Sentiment classification
Scalable polarity labelling for Twitter-native language
Sarcasm, root cause, service resolution, customer satisfaction, or financial impact




The selected model is trained on approximately 124 million tweets and fine-tuned for the TweetEval benchmark, making it a more appropriate baseline for this specific social-media domain than a generic sentiment default . AutoViz supports a configurable analysis-row cap, which is important when working with a corpus containing millions of records .

Repository Structure

Plain Text


customer-sentiment-twitter-executive/
├── data/
│   ├── sample.csv                         # Supplied 93-record working sample
│   └── README.md                          # Dataset handling and Git hygiene
├── notebooks/
│   └── customer_sentiment_twitter_executive.ipynb
├── src/
│   ├── run_analysis.py                    # Core analysis and curated charts
│   ├── run_autoviz.py                     # AutoViz implementation
│   ├── build_validation_pack.py            # Human-review queue
│   └── create_notebook.py                 # Rebuilds the notebook artifact
├── docs/
│   ├── executive_insights.md
│   ├── model_validation.md
│   └── source_notes.md
├── outputs/
│   ├── sample_analysis/                   # Reproducible sample results
│   ├── sample_autoviz/                    # Automated EDA artifacts
│   └── sample_validation/                 # Audit template and diagnostics
├── presentation/
│   └── slide_content.md
├── requirements.txt
├── .gitignore
└── README.md



Evidence from the Supplied Sample

The result below is intentionally scoped to the data included with this repository. It demonstrates the workflow, not the population.

Observation
Evidence
Interpretation
Observed tweets
93
Small working sample for a reproducibility demonstration.
Inbound customer tweets
49
Customer voice is isolated before sentiment scoring.
Negative sentiment
26 (53.1%)
The sample is dominated by customer-friction language.
Product and app performance theme
12 tweets, 9 negative
The largest named issue category in this slice.
Low-confidence classifications
7 (14.3%)
A controlled queue for manual review.
Sarcasm found in audit
At least one evident case
Sentiment labels cannot be used without contextual human review.




The full interpretation and management recommendations are available in docs/executive_insights.md. Model limitations and the qualitative audit are documented in docs/model_validation.md.

Reproduce Locally

Create a virtual environment, install the pinned dependencies, and run the core scripts. The workflow was validated with the supplied sample before delivery.

Bash


python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt

python src/run_analysis.py \
  --input data/sample.csv \
  --output-dir outputs/local_analysis \
  --max-inference-rows 50000

python src/run_autoviz.py \
  --scored-input outputs/local_analysis/scored_inbound_tweets.csv \
  --output-dir outputs/local_autoviz

python src/build_validation_pack.py \
  --input outputs/local_analysis/scored_inbound_tweets.csv \
  --output-dir outputs/local_validation



Quality and Governance Notes

This is a decision-support artefact. Sentiment is a modelled text signal, not a customer-satisfaction score. It must not be used as the sole basis for performance management, customer triage, or brand comparisons. The repository deliberately includes a human-review template and records that ground-truth accuracy is unavailable in the supplied data.

For a production workflow, add a reviewed issue taxonomy, explicit language detection, PII controls, human-label sampling, minimum-volume thresholds, trend baselines, and links to operational outcomes such as response time and resolution status.

References

[1] Kaggle: Customer Support on Twitter
[2] Google AI for Developers: Gemini API libraries
[3] Cardiff NLP: Twitter-RoBERTa sentiment model card
[4] AutoViz documentation
