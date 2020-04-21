# Where to find Brain MRI / NeuroImaging Datasets?

## Where to find Brain MRI / NeuroImaging Datasets?

Aggregated from [this question](https://www.researchgate.net/post/where_can_i_get_the_MRI_Brain_image_database_for_research_purpose) on ResearchGate.

* **OpenNEURO** : [https://openneuro.org/](https://openneuro.org/) \(formerly [OpenfMRI](https://openfmri.org/)\) - I would suggest starting with this.
* Connectome datasets -- A **connectome** \(/kəˈnɛktoʊm/\) is a comprehensive map of neural connections in the brain. \(via [Wikipedia](https://en.wikipedia.org/wiki/Connectome)\). Can contain **functional** connectivity and **anatomical** connectivity.
  * Human Connectome Project : [https://www.humanconnectome.org/](https://www.humanconnectome.org/) \(Sponsored by NIH; c.f. NDA\)
  * 1000 Functional Connectomes Project : [http://fcon\_1000.projects.nitrc.org/fcpClassic/FcpTable.html](http://fcon_1000.projects.nitrc.org/fcpClassic/FcpTable.html)
    * For Reliability and Reproducibility researches: [http://fcon\_1000.projects.nitrc.org/indi/CoRR/html/index.html](http://fcon_1000.projects.nitrc.org/indi/CoRR/html/index.html)
  * My Connectome Project - characterizes **changes over &gt;1 year** : [http://myconnectome.org/wp/](http://myconnectome.org/wp/)
* The Open Access Series of Imaging Studies \(OASIS\): [http://www.oasis-brains.org/](http://www.oasis-brains.org/)
  * See [this literature](https://www.medrxiv.org/content/10.1101/2019.12.13.19014902v1) for OASIS-3 dataset.
* University-based:
  * Center for Imaging Science, JHU: [http://www.cis.jhu.edu/data.sets/](http://www.cis.jhu.edu/data.sets/) \(high definition; **organized by cerebral regions**\)
  * Laboratory of NeuroImaging, USC: [https://ida.loni.usc.edu/](https://ida.loni.usc.edu/)
    * [Standardized MRI datasets](http://adni.loni.usc.edu/methods/mri-tool/standardized-mri-data-sets/), via [the Alzheimer’s Disease Neuroimaging Initiative](http://adni.loni.usc.edu/).
* SchizConnect: [http://schizconnect.org/](http://schizconnect.org/) - Aggregates datasets from the 5 websites: [fBIRN](https://www.nitrc.org/projects/fbirn/), [COINS](http://coins.mrn.org/), [XNAT Central](https://central.xnat.org/app/action/DisplayItemAction/search_value/NUDataSharing/search_element/xnat:projectData/search_field/xnat:projectData.ID), [NUNDA](https://nunda.northwestern.edu/nunda/data/projects/NMorphCH), and [NU REDCap](http://project-redcap.org/)
  * Collaborative Informatics and Neuroimaging Suite \(COINS\): [https://coins.trendscenter.org/](https://coins.trendscenter.org/)
    * Backed by: _Mind Research Network_, a nonprofit 501\(c\)3 organization Partnered with Lovelace Respiratory Research Institute
  * 04/18/2020: 3 out of 5 data sources are down. I suggest manually browsing these sources if you so desire.
  * This website is developed at the [Information Sciences Institute](https://www.isi.edu/) of USC. I wonder whether the collaborate with LONI \(see above\).

Some datasets I found interesting from OpenNEURO:

* \*\*\*\*[**28andMe**](https://openneuro.org/datasets/ds002674/versions/1.0.2): Daily MRI for a consecutive 30 days. [Reference](https://www.biorxiv.org/content/10.1101/866913v1).
* \*\*\*\*[**Deep Image Reconstruction**](https://openneuro.org/datasets/ds001506/versions/1.3.1): This is the [study](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1006633) where authors used Artificial Neural Network \(Deep Learning\) to reconstruct the images that the subject sees.
* \*\*\*\*[**Generic Object Decoding \(fMRI on ImageNet\)**](https://openneuro.org/datasets/ds001246/versions/1.2.1): visual features can be predicted from fMRI patterns, which in turn can be used to predict mental images \(which can be an imaginary image or something the subject is looking at\). [Reference](https://www.nature.com/articles/ncomms15037).

## Non-image data

There are other non-image data sources that might be of interest:

* Database for Emotion Analysis using Physiological Signals: [http://www.eecs.qmul.ac.uk/mmv/datasets/deap/](http://www.eecs.qmul.ac.uk/mmv/datasets/deap/) \(EEGs only; no MRI\)
* ~~AD临床前期联盟, China :~~ [http://www.alzheimer.org.cn/app/files/index](http://www.alzheimer.org.cn/app/files/index) \(Presents no data.\)
* NBDC Human Database, Japan: [https://humandbs.biosciencedbc.jp/](https://humandbs.biosciencedbc.jp/) \(mainly DNA sequences obtained with _illumina dye sequencing_\)
* The National Institute of Mental Health \(NIMH\) Data Archive \(NDA\), USA: [https://nda.nih.gov/](https://nda.nih.gov/)

## Tools

You might also be interested in related data-processing tools:

* [中国科学院心理研究所](http://yanlab.psych.ac.cn/) provides a set of tools：[http://rfmri.org/](http://rfmri.org/)
* [brainlife.io](https://brainlife.io/) offers many tools via in-browser VNC. I recommend mrView/[Mrtrix3](https://www.mrtrix.org/).

![](../.gitbook/assets/image%20%288%29.png)



