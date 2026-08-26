# deepCuisineTransfer

A recipe-text style-transfer autoencoder that rewrites cooking instructions between
Italian and Indian cuisine. A GRU encoder-decoder splits each recipe into a style
latent (cuisine) and a content latent (what's actually being cooked), trained with an
adversarial classifier to keep style information out of the content latent. At
inference, swapping in the target cuisine's average style vector and decoding produces
a style-transferred version of the recipe.


