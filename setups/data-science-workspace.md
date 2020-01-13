---
description: Describes how I usually set up my conda environment for data analytics.
---

# Data Science Workspace

I used to conduct data analysis, a lot. Nowadays? Not so much. Before I completely stop doing data-related work, it's probably a good idea to consolidate how my usual environment is set up.

You might be also interested in [my infrastructure for document-parsing projects](https://medium.com/dsmli/my-infrastructure-for-document-parsing-projects-4e2571b8f1de). Yes, I do have a Medium blog.

## Conda Environment

I use `conda` to manage my packages, mostly because it's language-agnostic and popular among data scientists. In terms of variants, I prefer `miniconda3` over Anaconda. This is because I would be creating virtual environments from scratch for each project anyways, and having a default environment with gigabytes of unused packages sounds like a waste. 

Here's some packages I generally install to every environment:

```bash
conda install jupyterlab # Provides main Web UI.
conda install pandas seaborn tqdm # The data science basics.
conda install requests # For retrieving data from Internet in Python, e.g. occasional web scraping.
conda install mongodb pymongo # When iteratively performing actions on multiple objects, I store temp variables in MongoDB, so as to avoid filling up memory.
```

Jupyterlab plugins to install:

* [Jupyterlab Code Formatter](https://jupyterlab-code-formatter.readthedocs.io/en/latest/installation.html)
* [Go to Definition](https://github.com/krassowski/jupyterlab-go-to-definition)
* [Collapsible Headings](https://github.com/aquirdTurtle/Collapsible_Headings)
* [Git](https://github.com/jupyterlab/jupyterlab-git)
* [GitHub](https://github.com/jupyterlab/jupyterlab-github)

## MongoDB

When iteratively performing actions on multiple objects, I store temporary variables in MongoDB, so as to avoid filling up memory. 

**Organization.** I maintain one instance of MongoDB server for each entity I work for \(e.g. WRDS, WWBP, and personal\). Within each instance, I use one _database_ for each project and one _collection_ for each type of temporary variable.

**Usage.** I usually organize code into cells that contain codes in the following form:

```python
collection = db['item']
criteria   = {}
N          = collection.count_documents(criteria)
cursor     = collection.find(criteria)
def work(doc):
    # ...
collection = db['itemCleaned190518']
with Pool(processes=40) as p:
    with tqdm(total=N, desc='Clean items') as pbar:
        for doc in p.imap_unordered(work, cursor): 
            pbar.update()
            collection.insert_one(doc)
```



