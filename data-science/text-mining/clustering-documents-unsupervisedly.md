---
description: A few thoughts and experiences on clustering documents with no supervision.
---

# On Clustering Documents Unsupervisedly

Say you have 1,000,000+ documents that you want to cluster. Your goal is to **explore if there are similar documents that can be hopefully grouped together**, which implies the following assumptions:

* **Undefined number of clusters**; ideally below 1,000; preferably 30~300.
* **90% documents are unique and cannot be clustered**; they can be seen as noise, or might form a single huge cluster, depending on how you look at it.

## Preprocessing

First of all, clean the data. Specifically, normalize frequently-used tokens. My favorite routine is to normalize URLs, dates, etc., using `TextPreProcessor` from [`ekphrasis`](https://github.com/cbaziotis/ekphrasis). 

{% hint style="info" %}
If text originates from a formal, business/governmental source, _normalization_ alone would be sufficient -- unpacking hashtags and correcting spellings won't be necessary.
{% endhint %}

I'm a huge word vector guy, so I'll first vectorize all documents into 300-dimensional vectors. Notice that I **do not deduplicate documents** before training Doc2Vec models, so that the Doc2Vec algorithm can have a more accurate feeling of which words are used together. \("Not applicable." repeating a million times means quite a lot for the two words, compared to this phrase only appearing once, right?\)

After training the Doc2Vec model, you can now group by cleaned text, count occurrences, and save that as a `weight` for each unique text.

## Clustering

For a noisy dataset with unknown geometry, I would always go for `DBSCAN` \(you can get a gut feeling why [here](https://scikit-learn.org/stable/modules/clustering.html)\). 

If you have only a couple of CPU cores to spare, try `HDBSCAN`. This is a variation of `DBSCAN`, does not seem to parallelize very well \(at least not with a convenient `n_jobs` parameter I can tamper with\), and appears to outperform \(read: halve computation time\) `sklearn.cluster.DBSCAN`: 

{% embed url="https://www.youtube.com/watch?v=AgPQ76RIi6A" %}

However, if you are working on a 24-core server, I found that **parallelism is king** -- I would rather go with `sklearn.cluster.DBSCAN` with `n_jobs` tuned up to full thrust \(`-1`\) rather than sticking with `HDBSCAN`.

{% hint style="info" %}
To be fair, `HDBSCAN` has a `core_dist_n_jobs` option for parallelization, but it seems to apply to only a small part of the computation, not contributing much to the overall time-saving.
{% endhint %}

However, `DBSCAN` got its own problem, too. It's memory complexity is `O(n^2)` and does not support caching \(compared to [agglomerative clustering](https://scikit-learn.org/stable/modules/clustering.html#hierarchical-clustering)\), rendering memory error even on a 250GB memory machine. The best I can do for now is to sub-sample my dataset to `10,000` documents and work from there.

{% hint style="info" %}
Some have proposed using `OPTICS` as a replacement, but -- same case with `HDBSCAN` and agglomerative clustering -- its `fit` method does not support `sample_weight`: This implies that, to get accurate clustering, you cannot deduplicate documents at all. In my case, that means 7x the amount of data. Not realistic.
{% endhint %}





