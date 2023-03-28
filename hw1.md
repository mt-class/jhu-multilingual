---
layout: default
img: dalle1.png
img_link: http://www.statmt.org/book/
title: Homework 2: Multilingual NLP
img2: dalle2.png
img2_link: http://www.statmt.org/nmt-book/
active_tab: main_page
---

Cross-Language Information Retrieval (CLIR)
===========================================

Cross-Language Information Retrieval has queries in one language and documents in another. Crossing the langauge barrier
is an integral part of the task. As we discussed in class, this is normally accomplished using three main methods:
* Translate Queries
* Translate Documents
* Project Both into a Shared Representation Space

Patapsco
--------

Patapsco is a python framework for CLIR experiments. You can find the GitHub repo for the project 
[here](https://github.com/hltcoe/patapsco). This is the [paper describing it](https://arxiv.org/abs/2201.09996).
This is a nice tool for running CLIR pipelines as you can specify in parameters in a yaml file. This
makes it easy to swap out different portions of the pipeline and run experiments using this.

For this Homework Assignment, we will be working from the [demo colab notebook](https://colab.research.google.com/github/hltcoe/patapsco/blob/master/samples/notebooks/demo-ecir.ipynb).
You are free to clone this notebook and run in another environment. However, running it in your browser should be sufficient
for this assignment. Run everything up until PSQ portion of the notebook. This should create a directory runs/query-translation/.
If you rerun portions, you will need to change the run name, or delete the previous run. It won't allow you to overwrite a run.
You should be able to find a scores.txt file after a run. As this is a very small, demo collection, we will not look at recall,
but instead report scores on MAP and NDCG Prime.

DELIVERABLES:
* Report map and ndcg_prime scores for test set 5 ( points)
* Report map and ndcg_prime scores for test set 6 ( points)

Query Translation
-----------------------------------

The first run was using human translated queries. We will now look at how different preprocessing steps impact the
translation. Note that as we discussed in class, modern neural methods for translation frequently break. Using human
translations is normally not possible at inference time, but is useful for evaluation of methods.

In the baseline run, both the documents and the queries are lowercased. First we will look at the impact of not
processing queries and documents in the same way. Change the queries to use truecase instead of lowercase.
The run should fail. Different preprocessing is such an issue for IR, that automatic checks like this are necessary.
Also change the document preprocessing to use truecased. Report MAP and NDCG Prime.

Change the tokenizer to stanza. Rerun the system using stanza and truecased.

DELIVERABLES:
* Report map and ndcg_prime scores for test set 5 using truecased queries and documents (5 points)
* Report map and ndcg_prime scores for test set 6 using truecased queries and documents (5 points)
* Talk about why these scores are what they are in comparison to the baseline (5 points)
* Report map and ndcg_prime scores for test set 5 using truecased queries and documents and stanza (5 points)
* Report map and ndcg_prime scores for test set 6 using truecased queries and documents and stanza (5 points)
* Talk about why these scores are what they are in comparison to the baseline (5 points)

PSQ
--------------

Probabilistic Structured Queries (PSQ) ([Darwish and Oard, 2003](https://dl.acm.org/doi/pdf/10.1145/860435.860497))
rely on statistical machine translation to create translation tables of queries. The colab notebook already
has a pretrained version called: zho_eng_clean_reduced_pdt.dict 

We are interested in the impact of translation quality on translations on PSQ. Please train another translation 
table following the example in GitHub:
[Running PSQ Using Patapsco](https://github.com/hltcoe/patapsco/tree/master/samples/translation-table).

This process can be slow (relying on Giza++). Feel free to use a smaller bitext (say 20k lines) even
though the performance will not be as good as the baseline experiment. You are free to use any publicly
available Chinese English dataset you would like. After creating a new translation
table for PSQ, rerun the system using this.

DELIVERABLES:
* Report map and ndcg_prime scores for test set 5 using the provided PSQ table (5 points)
* Report map and ndcg_prime scores for test set 6 using the provided PSQ table (5 points)
* Report which bitext you used for the PSQ (1 point)
* Train a new translation table and upload it to gradescope (4 points)
* Report map and ndcg_prime scores for test set 5 using your new PSQ table (5 points)
* Report map and ndcg_prime scores for test set 6 using your new PSQ table (5 points)
* Talk about why these scores differ from the baseline and how much translation quality impacts performance (3 points)


Propose Improvements
--------------------

There are a lot of ways that this could be improved.
This could be from improved tokenization schemes, better translations, segmentation, etc.
Propose and implement 2 methods.

DELIVERABLES:
* Report map and ndcg_prime scores for test set 5 using only the first improvement (8 points)
* Report map and ndcg_prime scores for test set 6 using only the first improvement (8 points)
* Report map and ndcg_prime scores for test set 5 using only the second improvement (8 points)
* Report map and ndcg_prime scores for test set 6 using only the second improvement (8 points)

Write-Up
========

Please write about 500 words on the assignment. Include disucssion about how and why the method fails,
systematic problems with query translation, additional potential fixes that may help, etc.
Also, please discuss how you expect this to behave on at least two other languages? How will language
family, morphology, script, etc. affect results?

DELIVERABLES:
* 500 word short answer (10 points)

