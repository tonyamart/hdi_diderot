## Authorship of HDI fragments (Fonds Vandeul)
  
This repository contains supplementary materials to the paper ... on the authorship of of selected fragments from *Histoire de deux Indes*.  
...
The corpus was compiled by Julian Csapo, the preprocessing and examination (code) done by Antonina Martynenko; pipeline for the tests by Artjoms Šeļa & AM.  
  
[Corpus](##Corpus)  
[Methodology](##Methodology)  
[FP-1772](##FP-1772)  
[FV-Results](##FV-Results)  

## Corpus
### Reference set
The corpus as well as the metadata were prepared by Julian Csapo. Corpus metadata is stored as `data/corpus_metadata.csv`. The files in the corpus are presented as one file = one book.  
All together the corpus comprises 175 books by 17 authors:  
Baudeau, Chastellux, Condorcet, Deleyre, d'Holbach, Diderot, Guibert, Jaucourt, Jussieu, La Grange, Meister, Morellet, Naigeon, Pechméja, Raynal, Rivière, Saint-Lambert.  

### Test set
The fragments from the HDI are collected from ARTFL project, the third edition of the HDI (1780). **Only** fragments from *Fonds Vandeul* were taken into consideration for the current study.  

Each fragment is supplied with the metadata on its appearance in different editions and inclusion in *Pensées détachées* and/or *Mélanges*. The metadata for fragments is stored as `data/fragments_attributions_cln.csv`.

#### Groups of segments tested
- Segments from different editions:  
  - appeared 1770 - not changed 1774 - not changed 1780  
  - appeared 1770 - changed 1774 - not changed 1780  
  - appeared 1770 - not changed 1774 - changed 1780  
  - appeared 1770 - changed 1774 - changed 1780  
  - appeared 1774 - not changed 1780  
  - appeared 1774 - changed 1780  
  - appeared 1780  
  
- Segments from Pénsées Détachées and Mélanges:
  - segments in pencil (PD)
  - segments in ink (M)
  - segments included in ink, but not in pencil (M without PD)
  
- Separate fragments:
  - Fragment 'Les avantages de la vie sauvage'
    
The analysis of the fragments in full can be found in `scr/`.

The steps on corpus creation and cleaning as well as segments manipulation are shown in `01_corpus_cleaning.qmd` and `02_corpus_overview.qmd` respectively.

## Methodology
The analysis is split according two main pipelines used. The first is Iterative sampling General impostors pipeline (_IterGI_; pipeline: Artjoms Šeļa; analysis done in R); the second: Bootstrap Distance Imposters (_BDI_; pipeline: Ben Nagy; analysis done in Python, visualisations in R).
  
**Preprocessing**
- OCR sources of the books differ, so we tried to clean most frequent errors (long-s issues, -oit => -ait endings, etc.);
- In the IterGI tests overlong books by each author were sampled down to 60k random tokens;  
  
**Methods testing**
- To see if methods work on this unbalanced and medium-quality corpus, number of "ground truth" tests were done. In these experiments, the works of known authors were considered as written by "unknown authors" and the algoriithms asked to perform attribution with the same settings as in real experiments. See the overview of results in `01_ground-truth_overview.md`. Although the figures presented in the paper are based on the analysis of word frequencies, the same series of experiments were conducted based on character 4grams frequencies, see the results in `2_ngrams_overview.md`.


Main part of the analysis: 
**Iterative sampling General Imposters**  
- For the main part of the analysis GI method was used (stylo implementation, cosine delta);
  - 100 trials of each GI test result in a coefficient between 0 and 1. This shows how many times an author was the closest to the text in question: 0 means 'in none of the trials', 1 means 'in all of the trials';  
- 100 iterations of GI test was performed, for each a new set of random independent samples was taken from the corpus;  
- The distribution of the 100 GI distributions (from 0 to 1) presented as box plots.  

**BDI**
- Standard implementation of BDI method: 
  - Consecutive chunks of 2000 words; 
  - Rel. frequencies of 200 MFW;
  - All authors and all works used.

## Main results
### Editions
Based on the current corpus, in all tests these segments demonstrate _no_ closeness to Diderot's writings. In some cases we found similarity to d'Holbach's writings. 

![plot-1770-nch](https://github.com/tonyamart/hdi_diderot/blob/main/scr/iter_GI/imp_res/0_plots_main/1_ed1770-nch-nch.png?raw=true) 

![bdi-short](https://github.com/tonyamart/hdi_diderot/blob/main/scr/plots_paper/fig_2-b.png?raw=true)

### PD vs M
In the case of red pencil marks our results are quite similar to that of the edition of 1770. There is quite a strong signal of d'Holbach authorship, although here the algorithm is less sure than in case of fragments from the earlier editions. 

![plot-PD](https://github.com/tonyamart/hdi_diderot/blob/main/scr/iter_GI/imp_res/0_plots_main/8_pencil.png?raw=true)

The observations on the word usage in *Mélanges* are more questionable, as this selection leads us to the mixed-authorship: sporadically some text fragments  resemble some of the authors from our corpus.

![plot-M](https://github.com/tonyamart/hdi_diderot/blob/main/scr/iter_GI/imp_res/0_plots_main/9_ink.png?raw=true)
![plot-bdi-m](https://github.com/tonyamart/hdi_diderot/blob/main/scr/plots_paper/fig_3-b.png?raw=true)
