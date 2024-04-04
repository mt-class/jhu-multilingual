---
layout: default
img: dalle1.png
img_link: http://www.statmt.org/book/
title: Homework 2: Multilingual NLP
img2: dalle2.png
img2_link: http://www.statmt.org/nmt-book/
active_tab: main_page
---

Isotropy - DUE APRIL 21 11:59PM
=========================================================

Multilingual neural models encode languages into a high-dimensional space. However, numerous work 
has shown that monolingual neural models frequently do not make use of every dimension. Isotropy 
is a measure of how the variance of a distribution is distributed across dimensions. In general, the field 
assumes that more isotropic models have better performance. Yet, there are numerous papers 
that argue both for and against this which we discussed in class. However, the majority of these 
works are monolingual. Little has been done in the multilingual setting. This homework assignment 
will have you measuring isotropy using different methods on various pre-trained multilingual models.


Definition
--------

We define isotropy using the [IsoScore paper](https://aclanthology.org/2022.findings-acl.262.pdf). A 
distribution is isotropic if:
* Variance is uniformly distributed across all dimensions
* Fully isotropic when the covariance matrix is proportional to the identity matrix

A distribution is anisotripic when the variance is dominated by a single dimension.


An Isotropy Analysis in the Multilingual BERT Embedding Space
-------------------------------------------------------------

We first look at isotropy in mBERT defined in [Rajaee and Pilehvar 2022](https://arxiv.org/pdf/2110.04504.pdf).
This paper looks at two measures of isotropy, cosine similarity and principal components.
In general, the results of this paper sugges that mBERT is highly anisotropic despite not having a single
outlier dimension. Broadly, BERT is found to be more isotropic than mBERT.

We first use the defintions of Isotropy from this paper, which relies on two previous works:
* Cosine Similarity (Ethayarajh 2019)
* Principal Components (Mu and Viswanath 2018)

Formal definitions are found in Section 2.1 of Rajaee and Pilehvar (2022). For the first part of this 
assignment, you will replicate part of the experiments from this paper. You are free to use 
[the code provided](https://github.com/Sara-Rajaee/Multilingual-Isotropy/blob/main/code/Analysis_Multilingual_notebook.ipynb) 
by the authors. Calculate the isotropy on the provided English and Spanish data in the repo.

Choose another language that is in mBERT, but was not evaluated in the paper. You will need to 
create a CSV file with roughly 3,000-5,000 lines in the language. Make sure to report all sources, preprocessing 
steps, and other information needed to replicate results.

DELIVERABLES:
* Report I_PC and Cosine Similarity for English (5 points)
* Report I_PC and Cosine Similarity for Spanish (5 points)
* Report I_PC and Cosine Similarity for an additional language (10 points)
* Talk about how your new language compares to the published results (10 points)


An Isotropy Analysis in the XLM-R Embedding Space
-------------------------------------------------------------

However, one of the main arguments for investigating isotropy is that more isotropically distributed models 
perform better. We may expect the converse to be true. We therefore would expect a better performing model to 
be more isotropic. Since XLM-R generally performs better than mBERT on many downstream tasks, we would hypothesize 
it would have more isotropic distributions. Rerun the previous results swapping out XLM-R for mBERT. Remember 
to change tokenizers as well.

DELIVERABLES:
* Report I_PC and Cosine Similarity for English (5 points)
* Report I_PC and Cosine Similarity for Spanish (5 points)
* Report I_PC and Cosine Similarity for an additional language (5 points)
* Talk about how these XLM-R results compare to mBERT (5 points)

IsoScore
--------------

Rudman et al., (2022) propose [IsoScore](https://aclanthology.org/2022.findings-acl.262.pdf) and argue that 
most of the published work on isotropy is not using the proper mathematical definition. They run experiments 
on GPT, GPT-2, BERT, and DistillBERT, but do not run any multilingual experiments. For the rest of this assignment, 
you will rectify this. Fortunately for you, they provide a toolkit you can pip install. Their repo is 
[available here](https://github.com/bcbi-edu/p_eickhoff_isoscore). Caclulate the IsoScore on the three languages 
you have been using above. Make sure to report the dimension you are evaluating on (mBERT and XLM-R have different 
dimensions) and IsoScore is dependent on this. You can make use of 
[this code](https://github.com/TideDancer/iclr21_isotropy_contxt) to generate embeddings.

DELIVERABLES:
* Report IsoScore on mBERT on English (5 points)
* Report IsoScore on mBERT on Spanish (5 points)
* Report IsoScore on mBERT on additional language (5 points)
* Report IsoScore on XLM-R on English (5 points)
* Report IsoScore on XLM-R on Spanish (5 points)
* Report IsoScore on XLM-R on additional language (5 points)
* Talk about how IsoScore differs from I_PC and Cosine Similarity for both mBERT and XLM-R (10 points)


Write-Up
========

Please write about 500 words on the assignment. Include disucssion about how and why you see 
differences between the IsoSCore and the other methods. Which do you think is a better 
measure of isotropy? Is isotropy actually worth measuring for multilingual settings? 
Discuss what you think would be a useful takeaway from this line of work for the field. 
Propose a potential improvement for either scoring, or using these scores (very broad, no correct answer).

DELIVERABLES:
* 500 word short answer (10 points)

