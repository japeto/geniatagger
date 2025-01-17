
# GENIA Tagger

Tsujii laboratory
University of Tokyo


Analyzes English sentences and outputs the base forms, part-of-speech tags, chunk tags, and named entity tags. The tagger is specifically tuned for biomedical text such as MEDLINE abstracts. If you need to extract information from biomedical documents, this tagger might be a useful preprocessing tool.


## How to build 
You need gcc to build the tagger.

% make

if you encounter errors with hash, try commenting out "#define USE_HASH_MAP" in "maxent.h".


## How to use

Prepare a text file containing one sentence per line, then

% ./geniatagger < TEXTFILE > TAGGEDTEXT

The tagger outputs the base forms, part-of-speech (POS) tags, chunk tags,
and named entity (NE) tags in the following tab-separated format.

word1	base1	POStag1	chunktag1 NEtag1
word2	base2	POStag2	chunktag2 NEtag2
  :     :        :       :

Chunks and named entities are represented in the IOB2 format (B for BEGIN,
I for INSIDE, and O for OUTSIDE). The named entity tagger is trained on
the NLPBA data set [3], which contains five semantic classes (DNA, RNA,
cell_line, cell_type, and PROTEIN).


## Tokenization

This tagger tokenizes the sentence with almost the same policy as the
upenn tokenizer (http://www.cis.upenn.edu/~treebank/tokenizer.sed). 

If you don't want the tagger to perform tokenization, use -nt option.
In that case, the input sentences should be already tokenized by your
own tokenizer with white spaces. 


## Sample
sentence = "Recombinant MIP-1-alpha induces a dose-dependent inhibition of different strains of HIV-1, HIV-2, and simian immunodeficiency virus (SIV)."

./geniatagger

> paste sentence in terminal.


    Recombinant         Recombinant         JJ        B-NP      B-protein 
    MIP-1-alpha         MIP-1-alpha         NN        I-NP      I-protein 
    induces             induce              VBZ       B-VP      O         
    a                   a                   DT        B-NP      O         
    dose-dependent      dose-dependent      JJ        I-NP      O         
    inhibition          inhibition          NN        I-NP      O         
    of                  of                  IN        B-PP      O         
    different           different           JJ        B-NP      O         
    strains             strain              NNS       I-NP      O         
    of                  of                  IN        B-PP      O         
    HIV-1               HIV-1               NN        B-NP      O         
    ,                   ,                   ,         O         O         
    HIV-2               HIV-2               NN        B-NP      O         
    ,                   ,                   ,         O         O         
    and                 and                 CC        O         O         
    simian              simian              JJ        B-NP      O         
    immunodeficiency    immunodeficiency    NN        I-NP      O         
    virus               virus               NN        I-NP      O         
    (                   (                   (         O         O         
    SIV                 SIV                 NN        B-NP      O         
    )                   )                   )         O         O         
    .                   .                   .         O         O         




## References

[1] Yoshimasa Tsuruoka and Jun'ichi Tsujii, Bidirectional Inference with
    the Easiest-First Strategy for Tagging Sequence Data, Proceedings of
    HLT/EMNLP 2005, pp. 467-474.

[2] Yoshimasa Tsuruoka, Yuka Tateishi, Jin-Dong Kim, Tomoko Ohta, John
    McNaught, Sophia Ananiadou, and Jun'ichi Tsujii, Developing a Robust
    Part-of-Speech Tagger for Biomedical Text, Advances in Informatics -
    10th Panhellenic Conference on Informatics, LNCS 3746, pp. 382-392, 2005

[3] http://research.nii.ac.jp/~collier/workshops/JNLPBA04st.htm

Please send questions and comments to tsuruoka@is.s.u-tokyo.ac.jp.
---------------------------------
Tsujii laboratory,
Department of Computer Science,
University of Tokyo
http://www-tsujii.is.s.u-tokyo.ac.jp/
