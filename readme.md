## Authorship of HDI fragments (Fonds Vandeul)
  
This is the repository for the article **Ghostwriting and Collective Authorship in the Enlightenment: Denis Diderot, d’Holbach’s Coterie, and the Problem of Authorship in Raynal’s *Histoire des deux Indes***.  
  
The corpus was compiled by Julian Csapo, the preprocessing and examination (code) done by Antonina Martynenko; pipeline for the tests by Artjoms Šeļa & AM.  
  
The data and metadata used for analysis can be found in the folder `data`. Reference set metadata is stored as `data/corpus_metadata.csv`, problems set (HDI framgets) metadata is placed at `data/fragments_attributions_cln.csv`.  
  
The code used for computational analysis of the fragments in full can be found in `scr/`.  
The steps on corpus creation and cleaning as well as segments manipulation are shown in `01_corpus_cleaning.qmd` and `02_corpus_overview.qmd` respectively.  
The analysis folders are split according to the two main pipelines used. The first is Iterative sampling General impostors pipeline (_IterGI_; analysis done in R); the second: Bootstrap Distance Imposters (_BDI_; analysis done in Python, visualisations in R).  
  
In addition to the main results described in the paper, the repository contains test results for character ngram analysis (see `2_ngrams_overview.md` and notebooks titled as *ngrams*) as well as multiple ground truth tests (see `1_ground-truth_overview.md` and correspoding notebooks).  
  
The figures used in the publication are in `scr/plots_paper`, additional figures obtained with each method can be found in the respective `scr` folders.  
  
  