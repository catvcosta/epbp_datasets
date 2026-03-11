# A Comparison of Methods to Bias Translation Toward Portuguese Variants

This repository contains datasets used in experiments described in the paper "A Comparison of Methods to Bias Translation Toward Portuguese Variants". The data includes processed subsets of the **FRMT dataset**, curated splits derived from **Tatoeba** datasets, and manually evaluated examples contrasted with the evaluations from the classifier we used, the PeroVaz_PT-BR_Classifier.

## frmt/

This folder contains the **processed version of the FRMT dataset** used in the experiments.

The original FRMT datasets were split at the **document level** into *exemplar*, *dev*, and *test* splits. During dataset inspection prior to the experiments, several issues were identified:

- Some sentences were **not properly segmented**.
- For the purposes of this research, the **exemplar** and **dev** buckets were more useful when **combined for fine-tuning**.

After cleaning and restructuring the data:

- **2847 sentences** were used in the **development set**, which served as fine-tuning data.
- **2597 sentences** were kept in the **test set**, which was translated by all evaluated systems and used for computing evaluation metrics.

The development data was used both **alone** and **combined with different subsets of the Tatoeba dataset**.

## tatoeba_data/

This folder contains curated **English–Portuguese subsets derived from the Tatoeba dataset**.

Several versions of this dataset exist, and Portuguese translations are typically **mixed between Brazilian Portuguese (BP)** and **European Portuguese (EP)**. To obtain a usable development corpus for variant-specific experiments, the following process was applied:

1. Start from the **2023 Tatoeba Portuguese dataset** (227,657 sentences).
2. Remove all sentence pairs that were present in **Portuguese datasets released before 2021**, which are likely included in the training data of the **OPUS-MT model** used as our baseline.
3. This filtering yielded **172,121 English–Portuguese sentence pairs** that the model had not previously seen.
4. Sentences were automatically classified as **BP or EP** using the **PeroVazPT-BR classifier**.
5. Two datasets of **50,000 sentences each** were created for the two variants.

For the **EP dataset**, each sentence was **manually verified and adapted where necessary**.

## manual_eval_100.txt

A set of **100 manually evaluated translation examples** used for qualitative analysis and comparison across translation methods.

## Purpose

These datasets were prepared to support experiments investigating **translation quality differences between European and Brazilian Portuguese** and to evaluate the impact of **fine-tuning on variant-specific data**.

They were used for:

- Fine-tuning machine translation models
- Automatic evaluation of translation quality
- Manual qualitative analysis
