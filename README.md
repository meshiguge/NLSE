NLSE
====
Non-Linear Sub-Space Embedding model used for the SemEval challenge described
in

    R. F. Astudillo, S. Amir,  W. Ling, B. Martins, M. Silva and I. Trancoso "INESC-ID: 
    Sentiment Analysis without hand-coded Features or Liguistic Resources using Embedding 
    Subspaces", SemEval 2015
    
for the extended experiments, including POS tagging, please cite

    R. F. Astudillo, S. Amir,  W. Ling, M. Silva and I. Trancoso "Learning Word Representations 
    from Scarce and Noisy Data with Embedding Sub-spaces", ACL-IJCNLP 2015

This code assumes that you posses the SemEval data from 2013 to 2015. You need
to tokenize the data using

    https://github.com/myleott/ark-twokenize-py

It should look like this example

    id1 id2 neutral None @USER i told you shane would get his 5th-star on rivals before signing day . @USER

Once you have formatted the data, you just have to run 

    ./go.sh

to train a model and obtain the baseline. If you want to carry out this steps
by yourself, you need to do the following

You should create the index and global vocabulary. For this you need to use

    python code/extract.py -f DATA/txt/semeval_train.txt \
                              DATA/txt/tweets_2013.txt \
                              DATA/txt/tweets_2014.txt \
                              DATA/txt/tweets_2015.txt \
                              DATA/pkl/ 

This store as DATA/pkl/semeval_train.pkl and create a global vocabulary for all
txt files in Pickel format under

    DATA/pkl

Note that this should also work with any number of input files as long as the
file format is respected.

Yo also will need to use some pre-trained embeddings. At the momment to get
our structured-skip-gram embeddings, you can reach us by email. Once you have
them, you can use

    python code/extract.py -e DATA/txt/struct_skip_50.txt \
                              DATA/pkl/struct_skip_50.pkl \
                              DATA/pkl/wrd2idx.pkl

To train the model use

    python code/train.py data/pkl/semeval_train.pkl \
                         data/pkl/dev.pkl \
                         DATA/pkl/struct_skip_50.pkl \
                         DATA/models/sskip_50.pkl

Get SemEval results

    python code/test.py DATA/models/sskip_50.pkl \
                        DATA/pkl/tweets_2013.pkl \
                        DATA/pkl/tweets_2014.pkl \
                        DATA/pkl/tweets_2015.pkl
