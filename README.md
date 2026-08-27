# deepCuisineTransfer

Text style transfer applied to recipes: given a recipe's instructions, transfer them from one cuisine's style (Italian) to another (Indian), while keeping the underlying cooking steps intact. Based on the disentanglement approach in [Deep Cuisine Transfer](127609301.pdf) (itself based on [John et al., 2019](https://aclanthology.org/P19-1041/)).

A GRU seq2seq autoencoder splits each recipe's instructions into a **style** latent (cuisine) and a **content** latent (the actual steps). Multi-task classifiers push each latent to actually capture its half of the split; adversarial classifiers - one per direction - push each latent to *not* leak the other half. To transfer a recipe, its content latent is decoded together with the *target* cuisine's average style latent instead of its own.

## Setup

Requires **Python 3.11** - `gensim` does not yet have a prebuilt wheel for 3.13/3.14, so a newer interpreter will fail to install it from `requirements.txt`.

```bash
python3.11 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Also needs Jupyter (`pip install jupyter`) to run the notebooks, and downloads the [Food.com recipes dataset](https://www.kaggle.com/datasets/shuyangli94/foodcom-recipes-with-search-terms-and-tags) via `kagglehub` on first run (no Kaggle credentials required for this dataset).

## Notebooks

Run in order:

1. **`preprocessing.ipynb`** - downloads and cleans the raw recipe data, filters to Italian/Indian recipes, tokenizes, splits into train/val/test, trains the Word2Vec embeddings, and fits the Bag-of-Words vectorizer. Saves everything under `data/` (gitignored - rerun this notebook to regenerate it locally). Word2Vec/BoW artifacts are only rebuilt if missing, so a saved model checkpoint doesn't silently go stale against a different vocabulary if you rerun this notebook.
2. **`model.ipynb`** - loads the artifacts `preprocessing.ipynb` produced, trains the GRU encoder/decoder with the multi-task + adversarial classifiers, performs style transfer, and scores it against a held-out test set and an independent evaluation classifier. Training is resumable - rerunning the training cell continues from the best checkpoint on disk instead of starting over.

`seq2seq_vocab.ipynb` is a separate, in-progress vocabulary/embedding exploration notebook.

## Data

`data/` is not committed. `preprocessing.ipynb` produces:
- `data/recipes_train.csv`, `data/recipes_val.csv`, `data/recipes_test.csv`, `data/recipes_final.csv`
- `data/models/word2vec.wordvectors`
- `data/models/bow_vectorizer.joblib`

`model.ipynb` additionally produces (also gitignored):
- `data/models/checkpoint.pt` (latest) and `data/models/checkpoint_best_recon.pt` (best by reconstruction loss - used for inference)
- `data/models/style_avg_italian.pt`, `data/models/style_avg_indian.pt`
- `data/style_transfer_results.csv`
