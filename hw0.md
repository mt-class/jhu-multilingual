---
layout: default
img: dalle1.png
img_link: http://www.statmt.org/book/
title: Homework 1: Multilingual NLP
img2: dalle2.png
img2_link: http://www.statmt.org/nmt-book/
active_tab: main_page
---

Silver Dataset Creation
=======================

Note: Start early! Some of these methods may take a while to run on your hardware and shared resources within the department
may be limited near the due date!

One of the major challenges with Multilingual NLP is the lack of resources in languages outside of English. An effective and popular way to deal with this is through "silver" datasets. These are automatically generated using various methods and algorithms from the field that leverage "gold" datasets (frequently available only in English). The goal of this assignment is to learn how to create a silver dataset using statistical word alignment with word-level English gold annotions. To be explicit, "gold" datasets are taken to be ground-truth and normally manually annotated by humans. These are assumed to be correct --- as humanly possible. Silver datasets are synthetically generated and attempt to create labels using automatic methods.

Multilingual Part-of-Speech Tagging
-----------------------------------

Part-of-speech tagging (POS) is a task where the words in a corpus are marekd by their corresponding speech tag (nouns, verbs, etc._.
In general, automatic POS taggers make use of labeled data from treebanks. These are expensive to create and while many efforts
to cover a wide-range of languages have been undertaken, there are only about 100 languages with easily usable treebanks.
You can see some of them through the [Universal Dependencies corpora](https://universaldependencies.org/).
In this assignment, we will create Silver POS tags for Swedish sentences using ONLY English labels. While Swedish POS annotated
treebanks exist, you are NOT ALLOWED to use them in this assignment. This is in order to simulate the low-resource cases
found for many NLP tasks in the majority of languages.

Word-Alignment
--------------

We will make use of statistical word-aligners - namely the IBM models ([Brown et al., 1993](https://aclanthology.org/J93-2003.pdf)).
We did not cover this in depth in class because most people said that they had seen this before (and even implemented it).
If you have questions, please contact the instructor and we can discuss this background in details.

We will use the GIZA++ implementation of the IBM models. These were created here at Hopkins during the summer JSALT workshop
during the last millenium. It is available on GitHub: [GIZA++](https://github.com/moses-smt/giza-pp). Instructions on how to run
it are in this [README](https://github.com/moses-smt/giza-pp/blob/master/GIZA%2B%2B-v2/README).

Tasks
=====

The assignment steps are broken down as follows:
* Train GIZA++ using [bitext.en](./hw0/bitext.en) and [bitext.sv](./hw0/bitext.sv)
* Use the word alignments from GIZA++ to project POS labels from English into Swedish
* Automatically generate new Swedish data and project labels
* Propose and implement two improvements to the pipeline
* Write-up results and discuss pitfalls as well as why things fail

Train GIZA++
------------

The first step is to run GIZA++ on the provided bitexts ([EN](./hw0/bitext.en) and [SV](./hw0/bitext.sv)). Follow the instructions from the repo above.
The format should be three lines for each example. For instance, a French-English example from GIZA++ looks like this:

"# Sentence pair (1)

il s' agit de la même société qui a changé de propriétaires

NULL ({ }) UNK ({ }) UNK ({ }) ( ({ }) this ({ 4 11 }) is ({ }) the ({ }) same ({ 6 }) agency ({ }) which ({ 8 }) has ({ }) undergone ({ 1 2 3 7 9 10 12 }) a ({ }) change ({ 5 }) of ({ }) UNK ({ })"


DELIVERABLES:
* For the first 10 sentences of the bitext provide the Alignment file (*.A3.*) for IBM Model 1 (5 points)
* Repeat for IBM Model 4 (5 points)


Project POS Alignments
----------------------

We have manually labeled part-of-speech tags for the first 3176 sentences of the English bitext.
These gold tags can be found here: [en_lines-ud-train.conllu](./hw0/en_lines-ud-train.conllu).
The file format is in the CoNLL-U format. The 4th column contains the manually
annotated POS Tag.
Use the alignment files from the previous step to project the tag onto the Swedish tokens.
Please format the projected alignments using the CoNLL-U format. There are freely available
paresers online for this format. If you use one, please reference it with proper ACL style
bibilographic citations as well as link to the repository.

DELIVERABLES:
* CoNLL-U file (.conllu) for IBM Model 1 Alignments on the first 3176 Swedish sentences (15 points)
* CoNLL-U file for IBM Model 4 Alignments (15 points)

Generate New Data
-----------------

We have 1032 lines of new English data that we want to project into Swedish here: [dev_pos_bitext.en](./hw0/dev_pos_bitext.en) 
and CoNLL-U file here: [en_lines-ud-dev.conllu](./hw0/en_lines-ud-dev.conllu).
Translate it into Swedish and re-run the first two steps. You can do this by
concatenating the 1032 lines onto the end of your bitexts. You can use any automatic
machine translation system for the transforming the raw English text into Swedish.
Again, please provide ACL style citations and a link to the translation system. If you
have built your own system, please note that here.

DELIVERABLES: 
* Translate English into Swedish automatically and provide translations (2 points)
* Run GIZA++ on new, larger bitext. Report IBM Models 1 & 4 Alignment scores on the same first 10 sentences (10 points)
* Write a 2-3 sentence paragraph as to why and how these scores have changed (3 points).
* Project English alignments from this file: onto your new Silver Swedish dataset and return the 1032 sentences in a CoNLL-U format (15 points)

Propose Improvements
--------------------

There are a lot of ways that this could be improved. This could be from better alignment models (IBM Models 5, [HMM](https://aclanthology.org/C96-2141.pdf), [AWESOME Align](https://github.com/neulab/awesome-align)), 
from data augmentation, dataset cleaning, etc. Propose and implement 2 methods.

DELIVERABLES:
* CoNLL-U file for 1032 sentences using new approach 1 (10 points)
* CoNLL-U file for 1032 sentences using new approach 2 (10 points)

Write-Up
========

Please write about 500 words on the assignment. Include disucssion about how and why the method fails,
systematic problems with this silver dataset creation, additional potential fixes that may help, etc.
Also, please discuss how you expect this to behave on at least two other languages? How will language
family, morphology, script, etc. affect results?

DELIVERABLES:
* 500 word short answer (10 points)

