# English–Greek Contrastive Dataset for Translation Error Detection

This repository contains the dataset and model scores associated with the paper:

**Evaluating Multilingual Sentence Embeddings for Translation Error Detection: An English–Greek Contrastive Study**

## Files

```text
data/
├── flores_en_el_contrastive_dataset.xlsx
└── english_greek_contrastive_model_scores.xlsx
```

**`flores_en_el_contrastive_dataset.xlsx`** contains 1,850 English–Greek contrastive examples with the English source sentence, correct Greek translation, erroneous Greek translation, and error category.

**`english_greek_contrastive_model_scores.xlsx`** contains the corresponding scores for each example from BGE-M3, Multilingual E5, Multilingual MPNet, LaBSE, Jina Embeddings v3, and COMETKiwi.

## Source Data

The contrastive dataset is derived in part from **FLORES+**.

The English source sentences and corresponding correct Greek reference translations originate from FLORES+. The erroneous Greek translations and error-category annotations were created as part of this study.

The final dataset contains **1,850 contrastive examples** based on **1,212 unique English–Greek FLORES+ sentence pairs**.

Users of this repository should consult the original FLORES+ resource and comply with its applicable licensing and attribution requirements.

FLORES+ dataset:  
https://huggingface.co/datasets/openlanguagedata/flores_plus

## Model Scores

The score file includes results from five multilingual sentence-embedding models:

- BGE-M3
- Multilingual E5
- Multilingual MPNet
- LaBSE
- Jina Embeddings v3

For these models, the file contains cosine-similarity scores for the correct and erroneous Greek translations.

The file also includes scores from **COMETKiwi**, used as a reference-free machine translation quality-estimation baseline.

COMETKiwi scores and embedding-model cosine similarities are defined on different numerical scales and should not be compared directly by their raw values or margin magnitudes.

## License

The FLORES+-derived content remains subject to the licensing and attribution requirements of the original FLORES+ dataset.

The controlled erroneous Greek translations, error annotations, and experimental model scores were produced as part of this study.

## Paper

The associated paper is available on arXiv:

**Evaluating Multilingual Sentence Embeddings for Translation Error Detection: An English–Greek Contrastive Study**

[View the paper on arXiv](https://arxiv.org/abs/YOUR_ARXIV_ID)

## Citation

If you use this dataset or the accompanying model scores, please cite:

```bibtex
@article{kalogeros2026translation,
  title   = {Evaluating Multilingual Sentence Embeddings for Translation Error Detection: An English--Greek Contrastive Study},
  author  = {Kalogeros, Eleftherios and Ntalakas, Athanasios and Gergatsoulis, Manolis and Nikolaou, Paschalis and Alexaki, Sotiria-Lito},
  journal = {arXiv preprint arXiv:YOUR_ARXIV_ID},
  year    = {2026}
}
```
