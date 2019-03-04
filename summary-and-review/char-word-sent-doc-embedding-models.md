---
description: >-
  Comparison of a few embedding algorithms used in natural language processing
  (NLP) tasks.
---

# 💬 Char/Word/Sent/Doc Embedding Models

| Name | vectorizes... | derived from | description |
| :--- | :--- | :--- | :--- |
| `word2vec` | word |  | give neighboring words, guess pivot word \(cbow\); or the other way around \(skip-gram\) |
| `doc2vec` | paragraph | `word2vec` | basically adding a paragraph vector to neighboring words while training |
| \`\`[`fastText`](https://github.com/facebookresearch/fastText)\`\` | sub-word n-grams | `word2vec` | can gen. sent. vec.s too, but [simply via sum & avg. ](https://github.com/facebookresearch/fastText/issues/26#issuecomment-363001444) |
| `GloVe` | word |  | works on **co-occurrence matrix** instead of training prediction models. [Surprisingly simil. to w2v](http://mlexplained.com/2018/04/29/paper-dissected-glove-global-vectors-for-word-representation-explained/). |
| \`\`[`BERT`](https://towardsdatascience.com/bert-explained-state-of-the-art-language-model-for-nlp-f8b21a9b6270)\`\` |  |  | [Transformer w/ self-attn](http://jalammar.github.io/illustrated-transformer/).; take whole doc. at once; \(1\) randomly masks out + replaces 10% words and try guess original; \(2\) try predict whether is next sent. VERY resource-hungry. |
| \`\`[`ELMo`](http://mlexplained.com/2018/06/15/paper-dissected-deep-contextualized-word-representations-explained/)\`\` | word |  | context-dep. bidirectional LSTM. |
| \`\`[`flair`](https://drive.google.com/file/d/17yVpFA7MmXaQFTe-HDpZuqw9fJlmzg56/view)\`\` | char |  | char-level, context-dep., LSTM. Looks cool but why so few mentions? |

There are also many sentence embedding algorithms that worth looking at: [https://medium.com/huggingface/universal-word-sentence-embeddings-ce48ddc8fc3a](https://medium.com/huggingface/universal-word-sentence-embeddings-ce48ddc8fc3a).



