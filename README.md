# iDeep

we proposed a deep learning based framework, iDeep, to fuse heterogeneous data for predicting RNA-protein interaction sites. The deep learning framework can
not only learn the hidden feature patterns from individual source of data, but also extracted the shared representation across them. In addition, the convolutional neural network in iDeep can automatically identify binding motifs. To validate our proposed method over other methods,
we perform experiments on large-scale CLIP-seq datasets. The comprehensive results indicated the huge advantage of iDeep, which performs much better than the state-of-the-art methods. 
 <br><br>
# Dependency <br>
<a href=https://github.com/fchollet/keras/>keras 1.2.0 library</a> and its backend is theano 0.9<br>
<a href=https://github.com/scikit-learn/scikit-learn>sklearn</a> <br>
<a href=http://www.h5py.org/>h5py</a>, install it using "pip install h5py" <br>
python 2.7 <br>

# Content <br>
./datasets: the training and testing dataset with extracted features, label and sequence. <br>
./cbust_folder: Cluster-buster tool is used to generate motif features. <br>
./pwms_folder: 102 PWMs from CISBP-RNA (Position Weight Matrix). <br>
./predicted_motifs: detected binding motifs for individual proteins from iDeep. and it also includes the report file ame.html from AME in MEME suite, it reporte the enrichment score for the predicted motifs. <br>
./ideep.py: the python code, it can be ran to reproduce our results. <br>
./make_feature_table.py: it is modified based on <a href=https://github.com/aertslab/primescore>primescore</a>. <br>

# Usage

 python ideep.py [-h] [--data_dir <data_directory>] [--train TRAIN] <br>
                [--model_dir MODEL_DIR] [--predict PREDICT] <br>
                [--out_file OUT_FILE] [--seq SEQ] [--region_type REGION_TYPE] <br>
                [--cobinding COBINDING] [--structure STRUCTURE] <br>
                [--motif MOTIF] [--batch_size BATCH_SIZE] <nr>
                [--n_epochs N_EPOCHS] <br> <br>
In our default setting, we will use seq, region_type, cobinding and structure, the features are generated by iONMF (https://github.com/mstrazar/iONMF). Thus, if you use default setting, the data_dir need have the following files:  sequences.fa.gz, 
matrix_RegionType.tab.gz, matrix_RNAfold.tab.gz, matrix_Cobinding.tab.gz, motif_fea.gz, and label file matrix_Response.tab.gz with 0 and 1. If you set the corrsponding option to be TRUE, you need have the corresponding data.

# Use example
<b>1.</b> Train the model using your data (currently only support fix-length sequences, it defaults to use sequence, region type, structure, clip cobidning modularity): <br>
python ideep.py --train=True --data_dir=datasets/clip/10_PARCLIP_ELAVL1A_hg19/5000/training_sample_0/ --model_dir=models
<br> <br>
--model_dir: the dir used to save the trained model, which is used for prediction step. <br>
 --data_dir configure your dir that contains <b>training</b> featrues file (sequences.fa.gz, matrix_RegionType.tab.gz, matrix_RNAfold.tab.gz, matrix_Cobinding.tab.gz) and label file (matrix_Response.tab.gz). <br>
<br>
<b>2.</b> predict the binding probability for your sequences (you need use the same dir for saved models in training step): <br>
 python ideep.py --predict=True --data_dir=datasets/clip/10_PARCLIP_ELAVL1A_hg19/5000/test_sample_0/ --model_dir=models --out_file=YOUR_OUTFILE
<br> <br>
--model_dir: The saved dir for models in training step. <br>
--data_dir: configure your dir that contains <b>testing</b> featrues file (sequences.fa.gz, matrix_RegionType.tab.gz, matrix_RNAfold.tab.gz, matrix_Cobinding.tab.gz), and the prediction probability for your sequences are saved in <YOUR_OUTFILE>, each line corresponds to the preobability of being RBP binding site for the sequence in fasta file.
<br>

<b>Reference</b> <br>
Xiaoyong Pan and Hong-Bin Shen. <a href=https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-017-1561-8>RNA-protein binding motifs mining with a new hybrid deep learning based cross-domain knowledge integration approach</a>. BMC Bioinformatics, 2017, 18:136. DOI: 10.1186/s12859-017-1561-8

Contact: Xiaoyong Pan (xypan172436atgmail.com)
