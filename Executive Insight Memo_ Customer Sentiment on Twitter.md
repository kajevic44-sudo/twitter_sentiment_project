# Executive Insight Memo: Customer Sentiment on Twitter

**Prepared for:** Armin Kajevic, Senior Management Consultant  
**Analysis basis:** Supplied `sample.csv`  
**Observed time window:** 10–12 October 2017 (UTC)  
**Purpose:** Demonstrate an AI-assisted workflow for understanding customer-support sentiment, not measure enterprise-wide performance.

## Executive Takeaway

The observed conversation slice is **customer-friction led**. Of the 49 inbound customer tweets scored with a Twitter-specialised RoBERTa classifier, **26 (53.1%) were negative**, **18 (36.7%) neutral**, and **5 (10.2%) positive**. The result is directionally useful for prioritising qualitative review, but it is not a valid benchmark for any company or for the complete Customer Support on Twitter corpus because the supplied file is a small, non-random extract.

| Observed measure | Result | Executive interpretation |
|---|---:|---|
| Total tweets | 93 | A small working sample, suitable for workflow validation rather than population-level claims. |
| Inbound customer tweets | 49 (52.7%) | Sentiment analysis correctly concentrates on the customer voice. |
| Outbound support replies | 44 (47.3%) | Reply context is retained for conversation-level follow-up. |
| Negative inbound sentiment | 26 (53.1%) | The sample contains a material concentration of friction signals. |
| Neutral inbound sentiment | 18 (36.7%) | Many messages are informational, diagnostic, or unresolved rather than overtly positive or negative. |
| Positive inbound sentiment | 5 (10.2%) | Positive confirmation exists but is limited in the observed slice. |

## What the Visual Exploration Adds

AutoViz generated six exploratory artifacts from a feature set containing support account, sentiment label, confidence, message length, UTC hour, weekday, and rule-based issue theme. Its target distribution independently surfaced the same **26 / 18 / 5** split. The automated output accelerated triage; however, it also underscored why executive interpretation cannot be automated. Its account-level comparisons are sensitive to tiny cell sizes, and encoded target labels are less suitable for a decision audience than curated charts.

The curated charts reveal a more actionable pattern. **Product and app performance** was the largest named issue theme, with 12 inbound tweets, of which 9 were classified as negative. **Connectivity and service outage** and **support access and communication** each accounted for five tweets, with three negative in each theme. The remaining 26 tweets fell into an explicitly labelled **Other / unclassified** bucket. This is a coverage gap in the transparent keyword heuristic, not evidence that the issues are insignificant.

| Named customer-issue theme | Inbound tweets | Negative tweets | Interpretation |
|---|---:|---:|---|
| Product & app performance | 12 | 9 | The clearest observed source of friction; prioritise defect, update, and performance review. |
| Connectivity & service outage | 5 | 3 | A smaller but operationally important signal requiring service-status context. |
| Support access & communication | 5 | 3 | Suggests friction in channels, status updates, or reachability. |
| Billing & account | 1 | 1 | Too small for a conclusion; retain in a broader monitoring taxonomy. |
| Other / unclassified | 26 | 10 | Do not treat as a business category; improve topic taxonomy or use human review. |

## Account-Level Signal: A Necessary Caveat

AppleSupport is associated with 17 inbound tweets in the sample, **82.4%** of which were classified as negative. This concentration is descriptive of the supplied records, not a company ranking. The sample includes only one to three inbound tweets for several accounts, and the dataset extract may have been selected around a particular episode. The presentation therefore shows brand comparisons only where the count is at least two and explicitly labels the conclusion as **sample-only**.

> **Decision rule:** A sentiment classifier identifies language polarity; it does not establish root cause, customer satisfaction, financial impact, severity, or service-level compliance. Those decisions require conversation context, operational data, and human review.

## Recommended Management Actions

First, use the workflow as an early-warning layer rather than a scorecard. A daily or weekly pipeline should flag negative and high-confidence inbound tweets, then route them for human validation. Second, blend sentiment with operational attributes such as product version, channel, response time, case resolution, and outage status. Third, replace the lightweight keyword themes with a governance-reviewed taxonomy, making the unclassified rate a measurable quality-control KPI. Fourth, report confidence intervals and minimum sample thresholds before comparing support accounts or time periods.

## How the AI Tools Contributed

| Tool | Productivity gain | Human judgment still required |
|---|---|---|
| Gemini | Converts a schema and data-quality profile into a rapid narrative of columns, missingness, and analytical priorities. | Validate all claims, decide which fields are meaningful, and ensure confidential data is not sent to an external model. |
| AutoViz | Produces a quick visual scan of distributions and relationships with a capped analysis sample. | Select decision-relevant charts, guard against spurious small-cell patterns, and explain context. |
| Hugging Face Twitter-RoBERTa | Scores Twitter-native language with negative, neutral, and positive classes at scale. | Review ambiguity, sarcasm, mixed sentiment, domain drift, and the distinction between polarity and business impact. |

## Method and Reproducibility Notes

The project accepts either the provided `sample.csv` or the full Kaggle `twcs.csv`. For a large file, it keeps descriptive counts on the loaded data and uses a fixed random seed when capping inference volume. The full Customer Support on Twitter dataset is sourced from Kaggle [1]. AutoViz supports a configurable row cap for large datasets [2]. The selected Cardiff NLP model is a Twitter-trained RoBERTa model fine-tuned for the TweetEval benchmark, making it a more defensible choice than a generic sentiment default for this task [3]. Gemini integration uses the current Google GenAI SDK and is optional because an API key is not embedded in the repository [4].

## References

[1]: https://www.kaggle.com/datasets/thoughtvector/customer-support-on-twitter "Kaggle: Customer Support on Twitter"
[2]: https://github.com/AutoViML/AutoViz "AutoViz documentation"
[3]: https://huggingface.co/cardiffnlp/twitter-roberta-base-sentiment-latest "Cardiff NLP: Twitter-RoBERTa sentiment model card"
[4]: https://ai.google.dev/gemini-api/docs/libraries "Google AI for Developers: Gemini API libraries"
