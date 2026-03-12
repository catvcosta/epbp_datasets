# A Comparison of Methods to Bias Translation Toward Portuguese Variants

This repository contains datasets used in the experiments described in the paper "A Comparison of Methods to Bias Translation Toward Portuguese Variants". The data includes processed subsets of the **FRMT dataset**, curated splits derived from **Tatoeba** datasets, and manually evaluated examples contrasted with evaluations from the PeroVaz_PT-BR_Classifier.

## frmt/

The original FRMT datasets consisted of English-Portuguese (European and Brazilian) pairs of sentences split into *exemplar*, *dev*, and *test* folders. During dataset inspection, prior to the experiments, several sentences were found not properly segmented and were therefore edited. The final edited sentences can be found in the ```dataset/``` folder.
After cleaning and restructuring the data:

- **2847 sentences** (exemplar and dev splits combined) served as fine-tuning data. Files ```EP_2.8K.tsv``` and ```BP_2.8K.tsv``` represent the FRMT data used in our fine-tuning experiments.

The development data was used both **alone** and **combined with different subsets of the Tatoeba dataset**.
   
- **2597 sentences** were kept in the **test set**. All evaluated systems translated these sentences, and the human-translated Portuguese versions of the FRMT test set served as the gold standard for computing evaluation metrics.

## tatoeba_data/

This folder contains curated **English–Portuguese subsets derived from Tatoeba datasets**.

Several versions of this dataset exist, and Portuguese translations are typically mixed between Brazilian Portuguese and European Portuguese. To obtain a usable corpus for variant-specific experiments, the following process was applied:

1. Start from the **2023 Tatoeba Portuguese dataset** (227,657 sentences).
2. Remove all sentence pairs that were present in the **Portuguese datasets released before 2021**, which are likely included in the training data of the **OPUS-MT model** used as our baseline.
3. This filtering yielded **172,121 English–Portuguese sentence pairs** that the model had not previously seen.
4. Sentences were automatically classified as **BP or EP** using the **PeroVaz_PT-BR_Classifier**.
5. Two datasets of **50,000 sentences each** were created for the two variants.

For the **EP dataset**, each sentence was **manually verified and adapted where necessary**.

From the 50K Tatoeba datasets, smaller subsets were created to test how much data was really necessary to provide the best fine-tuning results (10K and 2.8K subsets). For the same effect, the FRMT dev data was also combined with several splits of Tatoeba. All files with "tatoeba" in their name contain only Tatoeba data; the others are mixed with FRMT data.

## manual_eval_100.txt

A set of **100 random pairs of sentences** from the Tatoeba datasets, previously automatically classified by the PeroVaz_PT-BR_Classifier, was manually evaluated by one of the authors, a native speaker of European Portuguese. 84 sentences got the same label from both classification methods.

## References

Riley, Parker, Timothy Dozat, Jan A. Botha, Xavier Garcia, Dan Garrette, Jason Riesa, Orhan Firat, and Noah Constant. 2022. **FRMT: A Benchmark for Few-Shot Region-Aware Machine Translation**. *arXiv*. [https://arxiv.org/abs/2210.00193](https://arxiv.org/abs/2210.00193)

PeroVaz_PT-BR_Classifier [https://huggingface.co/bastao/PeroVaz_PT-BR_Classifier](https://huggingface.co/bastao/PeroVaz_PT-BR_Classifier)

Tatoeba Challenge [https://github.com/Helsinki-NLP/Tatoeba-Challenge](https://github.com/Helsinki-NLP/Tatoeba-Challenge)
