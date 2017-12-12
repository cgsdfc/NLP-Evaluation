# NLP-Evaluation
Scripts for some NLP evaluation tasks

## Monolingual Evaluation
### English Word Similarity Score and Word Similarity with Steigler's p-value 
Run the following command to evaluate the Word Similarity Score for many Word Simarity datasets:
```
python all_wordsim.py ~/mydir/your_vec data/word-sim/
```

This would output something like:
```
Vectors read from: ~/mydir/your_vec
=================================================================================
Serial              Dataset       Num Pairs       Not found             Rho
=================================================================================
     1   EN-RW-STANFORD.txt            2034            894         0.4325
     2         EN-RG-65.txt              65              0         0.6927
     3     EN-MTurk-771.txt             771              0         0.5719
     4     EN-MEN-TR-3k.txt            3000              1         0.6607
     5    EN-WS-353-ALL.txt             353              0         0.6229
     6        EN-YP-130.txt             130              0         0.3915
     7     EN-MTurk-287.txt             287              2         0.5856
     8      EN-VERB-143.txt             144              0         0.2562
     9         EN-MC-30.txt              30              0         0.6897
    10    EN-WS-353-SIM.txt             203              0         0.6849
    11    EN-SIMLEX-999.txt             999              1         0.4007
    12    EN-WS-353-REL.txt             252              0         0.5360
```
where the third cloumn is the Spearman’s rank correlation coefficient score

### Running Word Similarity with Steigler's p-value
Run the following over a pair of models for which you want to compute whether the difference is significant,
```
python stat_signf.py ~/mydir/en1.vectors ~/mydir/vulic_vectors/en2.vectors data/word-sim/EN-SIMLEX-999.txt
```

this will output something like,
```
Vectors read from: ~/mydir/en1.vectors
22
Vectors read from: ~/mydir/en2.vectors
23
==================================================
24
      Num Pairs       Not found             Rho
25
==================================================
26
         999              90          0.1234
27
         999              41          0.5678
28
         999             129          0.8429
29
(1.376206182800332, 0.014533569095982752)
```
Where the p-value is 0.014.

## Running BLDict

The dictionaries used for evaluation are provided in `en.*.dict`.

The format is,
`en1 en2 <tab> fr1 fr2 fr3`
Where `en1` and `en2` are entries on the english side which all share `fr1, fr2, fr3` as possible translations. For eg.

```dangerous hazardous unsafe risky        dangereux dangereuse```

If you compute the english side tokens of the dictionary you should get 1510 (fr), 1425 (de), 1610(zh) and 1024(sv).
