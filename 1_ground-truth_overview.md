This is a summary of additional experiments done for the HDI authorship problem. The main questions addressed with the experiments are: 

Part I. whether the methods work for texts with known authorship; 

Part II. whether other settings (e.g., other features) provide the same results as obtained with words. 

# Part I. Ground truth.

In this part I used our main pipelines in order to see if chosen methods will attribute works with known authorship to their true authors. The experiments have the same settings as applied to the problems later.

## Method I. Iterative sampling General Imposters.

For this experiment 5 authors (Diderot, d’Holbach, Baudeau, Condorcet, Raynal) were selected. For each author 5 works were randomly chosen to be analysed as “problems”. The whole corpus used for the attribution then. 

E.g., for d’Holbach the following 5 works were selected: “Éléments de la morale universelle”, “Histoire”, “La Morale”, “Le bon sens”. In the first iteration, I took the first work (”Éléments…”) and renamed it as written by an “unknown author”. Then the whole corpus was used to attribute the “Éléments…”; the desired outcome is evidently to obtain d’Holbach as the most probable author. Here are the results for 5 d’Holbach works (the boxplots more to the right mean better attribution):

![pic d’Holbach](https://github.com/tonyamart/hdi_diderot/blob/main/scr/iter_GI/imp_res/plots__authors_vs_all/dHolbach.png?raw=true)

The results are rather good for the rest of the authors (Please find the pictures here in the [github folder](https://github.com/tonyamart/hdi_diderot/tree/main/scr/iter_GI/imp_res/plots__authors_vs_all).

However the most important one for us—Diderot—actually demonstrated some problematic attributions. 

![pic Diderot - weird res](https://github.com/tonyamart/hdi_diderot/blob/main/scr/iter_GI/imp_res/plots__authors_vs_all/Diderot_weird%20results!!%20.png?raw=true)

With 5 more works by Diderot tested, it can be said that our algorithms are not totally wrong about finding Diderot's writings. However, sometimes there are issues with separating Diderot from Naigeon, Maister, and Marmontel.

![pic Diderot - additional](https://github.com/tonyamart/hdi_diderot/blob/main/scr/iter_GI/imp_res/plots__authors_vs_all/Diderot_additional.png?raw=true)

It is visible from the previous plots that some of the Diderot's writings are attributed to Naigeon. It may be explained by the fact that Naigeon was the editor of Diderot's works (?). We have only five works by Naigeon in our corpus, so I performed the same “masking” test for Naigeon to see, if we can catch his authorship signal correctly.

![pic naigeon](https://github.com/tonyamart/hdi_diderot/blob/main/scr/iter_GI/imp_res/plots__authors_vs_all/Naigeon.png?raw=true)

The results are not very robust: Naigeon's work “Le militaire philosophe” seems to be attributed to d’Holbach, the work “Manuel d’épictete” is very similar to Diderot, “Richesse” and “Unitaires” are close to Jaucourt. The number of words in each of these works is also not very high that can be problematic. In short, Naigeon's works may influence the attribution preciseness in whole. 

Another issue is with Meister's authorial corpus, where we have only two very short works (it is the smallest authorial sample in our corpus), so the comparison of target texts with his writings is unbalanced and may not be as robust. Lastly, it is hard to say why Marmontel is sometimes close to Diderot; Marmontel's subcorpus is large and heterogeneous enough, so the reasons for the similarity between him and Diderot should be studied further. 

Seeing these issues found in “ground truth” testing, in the main experiment we have two selections of authors: one is the corpus without “trouble-makers” (Naigeon, Meister, Marmontel), and the second is with them. This way we can see if anything would change in our results depending on these three authors. After comparing the results of the experiments done with/without Naigeon, Meister, and Marmontel, we can confirm that there is no strong influence and our main conclusions stay the same in both cases (plots for main selection: folder [imp_res/0_plots_main](https://github.com/tonyamart/hdi_diderot/tree/main/scr/iter_GI/imp_res/0_plots_main), selection that includes Naigeon, Meister, and Marmontel: [imp_res/1_plots_additional](https://github.com/tonyamart/hdi_diderot/tree/main/scr/iter_GI/imp_res/1_plots_additional)).

## Method II. BDI

In a similar way, the method was tested for the BDI. For selection of 5 authors (Diderot, d’Holbach, Baudeau, Condorcet, Raynal), 5 random works were taken and one work selected as a target (i.e., total 25 works in the corpus, not the whole selection — for time reasons). The algorithm was asked to show which authors are the closest to the problem (the distribution closer to the right side means better match). Here are results for d’Holbach and Diderot (rest of the results are in the [folder](https://github.com/tonyamart/hdi_diderot/tree/main/scr/bdi/03_tests/authors_vs_all/plots_5-authors)): 

Finding the attribution for d'Holbach's works (one column -- one work tested against five authors).  

![bdi d’holbach](https://github.com/tonyamart/hdi_diderot/blob/main/scr/bdi/03_tests/authors_vs_all/plots_5-authors/dHolbach.png?raw=true)
  
Finding the attribution for d'Holbach's works (one column -- one work tested against five authors).
  
![bdi Diderot](https://github.com/tonyamart/hdi_diderot/blob/main/scr/bdi/03_tests/authors_vs_all/plots_5-authors/Diderot.png?raw=true)

As in previous test, in some cases fragments from Diderot may be misattributed, but on average the distributions for his works are still by far more on the right sight then the others’. 

## FP (Fragment politique)

As part of the “ground truth” testing, we also used the FP fragment which is known to be written by Diderot. 

In case of Bootstrap consensus trees (word-based), we have *sometimes* results which indicate closeness to Diderot. However, the results on the BCT are unstable, so they are not used in further analysis.

![pic bct](https://github.com/tonyamart/hdi_diderot/blob/main/scr/iter_GI/imp_res/00_bct-fp_plots/FP_bct_4k_50-250mfw.png?raw=true)

### IterGI

In case of Iterative GI, Diderot is the closest author to FP in most of the cases. The dashed line shows the confidence interval, meaning that there is still some uncertainty suggested by the GI here.

![pic FP](https://github.com/tonyamart/hdi_diderot/blob/main/scr/iter_GI/imp_res/00_bct-fp_plots/FP_4k_200mfw.png?raw=true)
Iterative GI results for FP, 2000 words samples, 200 MFW

Not unexpectedly, the preciseness of the attribution is lower with lower number of words in a sample (cf.: [plot](https://github.com/tonyamart/hdi_diderot/blob/main/scr/iter_GI/imp_res/00_bct-fp_plots/FP_2k_200mfw.png?raw=true)).

### BDI

In the same fashion, FP fragment was attributed correctly by the BDI method with different settings: 

- 1000 words consecutive chunks:
    - frequencies of 100 MFW
    - frequencies of 200 MFW
- 2000 words consecutive chunks:
    - frequencies of 100 MFW
    - frequencies of 200 MFW

In all cases the Diderot's distribution was the one placed to the right side of the plot (100% of the distribution above 0). Increasing the number of words in chunk and/or number of MFW led to the distribution placement farer to the right: all results in the folder [(link)](https://github.com/tonyamart/hdi_diderot/tree/main/scr/bdi/03_tests/fp1).

![pic FP bdi results for 2k 200 mfw](https://github.com/tonyamart/hdi_diderot/blob/main/scr/bdi/03_tests/fp1/2000_words/fp1_2k_200MFW.png?raw=true)

In a way, FP results are better, than some of the known Diderot's works attribution performed above. In future, it would be interesting to examine multiple fragments of this kind (short & known for being by Diderot) and see, if they would show similar clear signal.

## Some conclusions

From all these tests altogether, we can confirm that BDI tends to place Diderot's and d’Holbach's works directly on the right, with very high percent (almost 100%) of the results above 0. 

E.g., these are results, if we use the whole corpus and see how known works are attributed to their true authors (nb. we do not see on these plots if any other author is also having the distribution placed on the right side; see the pic. 0. for comparison with other authors).

![pic author vs themselves - dHolbach](https://github.com/tonyamart/hdi_diderot/blob/main/scr/bdi/03_tests/authors_themselves/plots/dHolbach.png?raw=true)

![pic author vs themselves - Diderot](https://github.com/tonyamart/hdi_diderot/blob/main/scr/bdi/03_tests/authors_themselves/plots/Diderot.png?raw=true)

Iterative GI method (boxplots) also demonstrate the ability to reject false authors and find true ones for both FP and known works. 

As we will show in the main experiment, we have not obtain attributions of similar strength when testing HDI fragments.

