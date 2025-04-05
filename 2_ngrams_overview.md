# Part II. Ngrams

The main experiments conducted so far were based on counting word frequencies in different settings. However, it is a well-established practice in stylometry to use smaller elements of the text, in particular, to cut texts into sequencies of characters (character ngrams). It works as follows:

Example text: “Le chaume et la mousse verdissent les toits; La colombe y glousse, L'hirondelle y boit”

Word tokens: “Le” “chaume” “et” “la” “mousse” “verdissent” “les” “toits” “la” “colombe” “y” “glousse” “l” “hirondelle” “y” “boit” (16 words)

word frequencies: “la” - 2, “y” - 2, “boit” - 1, etc. 

Charater 4-gram tokens: "le_c" "e_ch" "\_cha" "chau" "haum" "aume" "ume_" "me_e" "e_et" "\_et_“ "et_l" "t_la" "\_la_“ "la_m" "a_mo" "\_mou" "mous" "ouss" "usse" "sse_“ etc. (83 ngrams total)

ngram frequencies: “\_la_" - 2, "e_y_" - 2, "ouss" - 2, "usse" – 2, "\_boi" - 1, "\_cha" – 1 , etc.

Although ngrams often make no sense to human reader (there is not much we can say about an author who use “usse” more or less frequently), it is known that character ngrams can catch smaller than words syntactic and morphological patterns (e.g., usage of a specific verb form ending with a preposition, such as in [e]“nt_y” or [o]“ns_à”; or prefixes such as “re-”). 

Using ngrams we also obtain more elements to count, as in the example with 16 words resulting in 83 ngrams. In real-case study, our 2,000 word chunks were turned in ~10,000 ngrams. What can be an obvious obstacle / bias here is the OCR quality (if some model consistently put “enf” instead of “ent”, we will find the model's “fingerpring”, not the author's one. However, we can always compare the ngram-based results with the word-based results, to see, if there is something suspicious or particularly different in either of the groups.

I replicated both Iterative-GI and BDI experiments with FP, Editions and Pencil/Ink fragments based on the frequencies of 500 most frequent ngrams (I also tested 200 MFN, it works but not as good).

None of our main conclusions was contradicted by ngram-based results, so I am just showing selected plots below. All pictures are available in the github folders `06_ngrams` [link](https://github.com/tonyamart/hdi_diderot/tree/main/scr/iter_GI/imp_res/plots_ngrams).

![1770-nch-nch-ngrams](https://github.com/tonyamart/hdi_diderot/blob/main/scr/iter_GI/imp_res/plots_ngrams/ed1770_nch1774_nch1780.png?raw=true)
Results for IterGI ngram-based test for fragments from ed1770 not changed later.

![ink_ngrams](https://github.com/tonyamart/hdi_diderot/blob/main/scr/iter_GI/imp_res/plots_ngrams/ink_melanges.png?raw=true)
Results for IterGI ngram-based test for fragments from _Mélanges_.

----

In case of BDI ngram results ([here](https://github.com/tonyamart/hdi_diderot/tree/main/scr/bdi/06_tests)), there are some chunks, which demonstrated interesting closeness to some candidates (except d’Holbach, that was already observed). E.g.:

![bdi-1770-nch-ch](https://github.com/tonyamart/hdi_diderot/blob/main/scr/bdi/06_tests/editions/plots/ed1770-nch-ch_2k_500MFN.png?raw=true)

Here _ed 1770-nch-ch_ shows interesting results for Raynal authorship

![bdi-1770-ch-ch](https://github.com/tonyamart/hdi_diderot/blob/main/scr/bdi/06_tests/editions/plots/ed1770-ch-ch_2k_500MFN.png)

Ed1770-ch-ch demonstrates that some fragments may be close to Diderot (but also we see a false positive with Condorcet, unfortunately). 
These preliminary findings need more examination in future, probably based on a better (i.e., cleaned and controlled) corpus.