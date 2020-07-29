---
description: Notes taken from attending SIGIR2020.
---

# Notes from SIGIR2020

## Talking with People

### Notes with Ameeta Agrawal

We talked about:

* Emotion lexica:
  * WEES
  * NRC/EmoLex
  * WNA
* Types of sarcasm:
  * Co-existence of positive and negative emotions in the text.
  * This is the type that was explored in Ameeta Agrawal's [work](https://dl.acm.org/doi/pdf/10.1145/3397271.3401183), _Leveraging Transitions of Emotions for Sarcasm Detection_.
  * I mentioned that the presence of transition words for opposition/contradiction may indicate genuine, impartial attempts to cover both sides of the argument \(consider IAC\).
  * Pointing out issues that should be common sense.
  * I talked about a real life example that happened at a closed car rental place.
  * Ameeta Agrawal suggested [COMET](https://arxiv.org/abs/1906.05317), a common sense KB, from U of Washington. \([GitHub](https://github.com/atcbosselut/comet-commonsense)\)

### Notes with Weixuan Zhang

Zhang is the author of the MUSE model. 3 types of document relationships:

* semantic relevance,
* textual entailment, and
* textual similarity.

### Notes with Suchana Datta

Author of [this](https://dl.acm.org/doi/pdf/10.1145/3397271.3401207).

* **On the change of the city name Bengalore to Bengaluru:** 
  * _Bangalore_ was the British spelling. In the local official language \(Kannada\), it is spelled _Bengaluru_.
  * This is similar to how _Calcutta_ was renamed to _Kolkata_.
* Resources for studying Indian language procesing:
  * [Dr. Pushpak Bhattacharyya](https://www.cse.iitb.ac.in/~pb/)
  * [CVPR at ISIC](https://www.isical.ac.in/~cvpr/)

### Notes with Maram Hasanain

* Datasets:
  * [ArabicWeb16: A New Crawl for Today’s Arabic Web](http://qufaculty.qu.edu.qa/telsayed/wp-content/uploads/sites/113/2016/05/spc312-suwaileh-1.pdf) \(note to self: see Table 2 for country-level dialect breakdown\) \([webpage](https://sites.google.com/view/arabicweb16/home?authuser=0)\)
  * [**ArTest**](https://dl.acm.org/doi/pdf/10.1145/3397271.3401223)**: For web search relevance benchmarking**
* Arabic-specific search engines: Yamli, Eiktub, and Yoolki
* [Farasa](http://alt.qcri.org/farasa/): text processing toolkit for Arabic \(note to self: supports diacritization!\)

## Other



### Copula \(probablity theory\)

* [Archimedean Couplas](https://www.vosesoftware.com/riskwiki/Archimedeancopulas-theClaytonFrankandGumbel.php)
  * Clayton Coupla -- easier to get probability distribution function
  * Frank Coupla
  * Gumbel Coupla
* Used in [this](https://dl.acm.org/doi/abs/10.1145/3397271.3401245) paper.

### Tabular-data-related projects

* [Summarizing and Exploring Tabular Data in Conversational Search](https://dl.acm.org/doi/pdf/10.1145/3397271.3401245):
* [SPot: A Tool for Identifying Operating Segments in Financial Tables](https://dl.acm.org/doi/pdf/10.1145/3397271.3401406): similar to my prior work at WRDS, with these differences:
  * 8-K instead of 10-K
  * parsing XML/HTML instead of plain text
* [Web Table Retrieval using Multimodal Deep Learning](https://dl.acm.org/doi/pdf/10.1145/3397271.3401120): record, schema, and facet.

### Work similar to our workshop paper

* [Recipe Retrieval with Visual Query of Ingredients](https://dl.acm.org/doi/pdf/10.1145/3397271.3401244)

### Search-engine-related projects

* [Supporting Interoperability Between Open-Source Search Engines with the Common Index File Format](https://dl.acm.org/doi/pdf/10.1145/3397271.3401404): uses protobuf
* [JASSjr: The Minimalistic BM25 Search Engine for Teaching and Learning Information Retrieval](https://dl.acm.org/doi/pdf/10.1145/3397271.3401413): written by the original author of JASS, JASSjr is only 400 lines of C++ code.

  **Ranking**

* OpenNIR: the framework upon which the code for [Expansion via Prediction of Importance with Contextualization](https://dl.acm.org/doi/pdf/10.1145/3397271.3401262) was built upon. Also written single-handedly by Sean MacAvaney.
* Works by Omar Khattab:
  * `ColBERT`: Efficient and Effective Passage Search via Contextualized Late Interaction over BERT

      My follow-up question was: _Are the queries padded by **appending** \[MASK\] tokens to the orginal tokens only? I wonder what happens if you insert \[MASK\] tokens randomly \*between_ the orginal tokens. Intuitively, it would probably enhance the robustness of ColBERT to variations of the same query.

    * Finding the Best of Both Worlds: Faster and More Robust Top-k Document Retrieval
    * Efficient Document Re-Ranking for Transformers by Precomputing Term Representations

### Concepts I learned

* Crowdsourcing platforms in Japan:
  * `Lancers.jp`
    * Used in this work: [Crowdsourced Text Sequence Aggregation based on Hybrid Reliability and Representation](https://dl.acm.org/doi/pdf/10.1145/3397271.3401239).
  * `Crowdsourcing.yahoo.jp`
* Curriculum Learning
* The_Cranfield Paradigm_
* Package for extracting topics/topic modeling:
  * _Biterm Topic Model_ \(_BTM_\): word co-occurrence based topic model
    * [GitHub](https://github.com/bnosac/BTM), [R](https://rdrr.io/cran/BTM/man/BTM.html)
    * Gensim is also designed for topic modeling; I have been using it solely for training word embedding models though.
    * [_latent Dirichlet allocation_ \(_LDA_\)](https://en.wikipedia.org/wiki/Latent_Dirichlet_allocation):
  * Text Retrieval Conference \(TREC\): A program of NIST. De-facto standard of benchmarking IR work.
  * Some metrics:
    * [Kendal rank correlation coefficient "tau"](https://en.wikipedia.org/wiki/Kendall_rank_correlation_coefficient): ordinal association
    * [BM25](https://en.wikipedia.org/wiki/Okapi_BM25): [bag-of-words](https://en.wikipedia.org/wiki/Bag_of_words_model) retrieval function that ranks a set of documents based on the query terms appearing in each document. \(from Wikipedia\)
      * BM = "best matching"

