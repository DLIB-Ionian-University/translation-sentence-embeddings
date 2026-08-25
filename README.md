English–Greek Contrastive Dataset for Translation Error Detection
This repository contains the dataset and experimental model scores associated with the paper:
Evaluating Multilingual Sentence Embeddings for Translation Error Detection: An English–Greek Contrastive Study
The study investigates whether general-purpose multilingual sentence-embedding models can distinguish correct English–Greek translations from minimally modified translations containing controlled errors. It also compares the embedding models with the reference-free COMETKiwi machine translation quality-estimation model.
Repository Contents
```text
data/
├── flores_en_el_contrastive_dataset.xlsx
└── english_greek_contrastive_model_scores.xlsx
```
The two files can be linked using:
```text
split + flores_id + error_category
```
This combination is important because the same FLORES+ sentence may appear in more than one error category.
---
1. Contrastive Dataset
`flores_en_el_contrastive_dataset.xlsx`
This file contains the English–Greek contrastive dataset constructed from sentence-aligned FLORES+ data.
The dataset contains:
1,850 contrastive examples
1,212 unique English–Greek FLORES+ sentence pairs
10 core error categories
5 exploratory error categories
Each example consists of:
an English source sentence;
its correct Greek FLORES+ reference translation;
a minimally modified Greek translation containing one controlled translation error; and
the corresponding error category.
A source sentence may occur in more than one example when different controlled error variants were constructed for different error categories.
Dataset Columns
Column	Description
`split`	FLORES+ split from which the sentence originates (`dev` or `devtest`).
`flores_id`	Identifier of the sentence within the corresponding FLORES+ split.
`source_en`	English source sentence from FLORES+.
`correct_el`	Correct Greek FLORES+ reference translation.
`incorrect_el`	Greek translation containing the controlled translation error.
`error_category`	Translation-error category assigned to `incorrect_el`.
Error Categories
The dataset covers 15 translation-error categories.
Core categories
Each core category contains 150 examples.
Negation
Number
Named entity
Antonym
Omission
Unsupported addition
Hallucination
Tense and aspect
Modality
Semantic role
Exploratory categories
Date and time — 75 examples
Unit and currency — 50 examples
Terminology — 75 examples
Pronoun and coreference — 75 examples
Discourse connective — 75 examples
The erroneous Greek translations were constructed collaboratively by two translation experts. Each final erroneous translation was reviewed and approved by both experts to verify that it contained the intended error, belonged to the assigned category, differed semantically from the correct reference translation, and remained sufficiently fluent and natural in Greek.
---
2. Experimental Model Scores
`english_greek_contrastive_model_scores.xlsx`
This file contains the scores produced by the evaluated methods for all 1,850 contrastive examples.
The first three columns identify the corresponding dataset example:
Column	Description
`split`	FLORES+ split (`dev` or `devtest`).
`flores_id`	FLORES+ sentence identifier.
`Error Category`	Controlled translation-error category.
The remaining columns contain separate scores for the correct and erroneous Greek translations.
Multilingual Sentence-Embedding Models
Five multilingual sentence-embedding models were evaluated:
Model	Checkpoint
BGE-M3	`BAAI/bge-m3`
Multilingual E5	`intfloat/multilingual-e5-large`
Multilingual MPNet	`sentence-transformers/paraphrase-multilingual-mpnet-base-v2`
LaBSE	`sentence-transformers/LaBSE`
Jina Embeddings v3	`jinaai/jina-embeddings-v3`
For each embedding model, the results file contains:
the cosine similarity between the English source and the correct Greek translation; and
the cosine similarity between the English source and the erroneous Greek translation.
The contrastive margin is defined as:
[
\Delta = \mathrm{sim}(\mathrm{source}, \mathrm{correct}) -
\mathrm{sim}(\mathrm{source}, \mathrm{error})
]
A positive margin indicates that the model assigns a higher cosine similarity to the correct translation. A negative margin indicates that the erroneous translation receives the higher similarity.
COMETKiwi
The results file additionally contains scores from the reference-free machine translation quality-estimation model:
COMETKiwi — `Unbabel/wmt22-cometkiwi-da`
For each contrastive example, COMETKiwi independently scores:
the correct Greek translation given the English source; and
the erroneous Greek translation given the English source.
The COMETKiwi contrastive margin is defined as:
[
\Delta_{\mathrm{COMETKiwi}} =
\mathrm{score}(\mathrm{correct}) -
\mathrm{score}(\mathrm{error})
]
A positive value indicates that COMETKiwi assigns a higher quality score to the correct translation.
> **Important:** COMETKiwi quality-estimation scores and embedding-model cosine similarities are defined on different numerical scales. Their raw score values and margin magnitudes should therefore not be compared directly across methods.
Score File Columns
Column	Description
`split`	FLORES+ split (`dev` or `devtest`).
`flores_id`	FLORES+ sentence identifier.
`Error Category`	Controlled translation-error category.
`BGE-M3 en-el correct`	Cosine similarity between the English source and the correct Greek translation using BGE-M3.
`BGE-M3 en-el error`	Cosine similarity between the English source and the erroneous Greek translation using BGE-M3.
`Multilingual E5 en-el correct`	Cosine similarity between the English source and the correct Greek translation using Multilingual E5.
`Multilingual E5 en-el error`	Cosine similarity between the English source and the erroneous Greek translation using Multilingual E5.
`Multilingual MPNet en-el correct`	Cosine similarity between the English source and the correct Greek translation using Multilingual MPNet.
`Multilingual MPNet en-el error`	Cosine similarity between the English source and the erroneous Greek translation using Multilingual MPNet.
`LaBSE en-el correct`	Cosine similarity between the English source and the correct Greek translation using LaBSE.
`LaBSE en-el error`	Cosine similarity between the English source and the erroneous Greek translation using LaBSE.
`Jina Embeddings v3 en-el correct`	Cosine similarity between the English source and the correct Greek translation using Jina Embeddings v3.
`Jina Embeddings v3 en-el error`	Cosine similarity between the English source and the erroneous Greek translation using Jina Embeddings v3.
`COMETKiwi en-el correct`	COMETKiwi quality-estimation score for the correct Greek translation, using the English sentence as source.
`COMETKiwi en-el error`	COMETKiwi quality-estimation score for the erroneous Greek translation, using the English sentence as source.
---
Evaluation
For every contrastive example, a method succeeds when it assigns a higher score to the correct Greek translation than to the erroneous Greek translation.
For the sentence-embedding models, this corresponds to:
```text
cosine_similarity(source_en, correct_el)
>
cosine_similarity(source_en, incorrect_el)
```
For COMETKiwi, this corresponds to:
```text
COMETKiwi(source_en, correct_el)
>
COMETKiwi(source_en, incorrect_el)
```
Contrastive accuracy is the proportion of examples for which the correct translation receives the higher score.
---
Source Data
The English source sentences and correct Greek translations originate from FLORES+.
The `incorrect_el` translations and their error-category annotations were created as part of this study to construct the English–Greek contrastive challenge set.
FLORES+ is not created or owned by the authors of this repository. Users should consult the original FLORES+ resource and comply with its applicable licensing and attribution requirements.
---
Citation
If you use this dataset or the accompanying model scores in academic work, please cite:
```bibtex
@article{kalogeros2026translation,
  title   = {Evaluating Multilingual Sentence Embeddings for Translation Error Detection: An English--Greek Contrastive Study},
  author  = {Kalogeros, Eleftherios and Ntalakas, Athanasios and Gergatsoulis, Manolis and Nikolaou, Paschalis and Alexaki, Sotiria-Lito},
  year    = {2026}
}
```
The citation information can be updated with the final publication details once available.
---
License
Please see the `LICENSE` file for the licensing terms applicable to materials created as part of this project.
The underlying FLORES+ source sentences and reference translations remain subject to the licensing and attribution terms of the original FLORES+ dataset.
---
Acknowledgements
This work uses sentence-aligned English–Greek data from FLORES+ and publicly available multilingual models distributed through Hugging Face.
The evaluated methods are:
BGE-M3
Multilingual E5
Multilingual MPNet
LaBSE
Jina Embeddings v3
COMETKiwi
