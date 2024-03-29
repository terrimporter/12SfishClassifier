# 12S MitoFish Reference Set For The RDP Classifier  

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.4741464.svg)](https://doi.org/10.5281/zenodo.4741464)  

This repository contains trained reference sets that can be used with the Ribosomal Database Project classifier (Wang et al., 2007) to taxonomically assign fish 12S mitochondrial gene sequences.  The latest releases can be downloaded from https://github.com/terrimporter/12SfishClassifier/releases

## Note

This classifier is suitable for classifying fish 12S mitochondrial gene sequences to genus rank.  Reference sequences were obtained from the Mitochondrial Genome Database of Fish (MitoFish) at http://mitofish.aori.u-tokyo.ac.jp/ (Sato et al., 2018) and the sequences for the 12S gene region was retrieved.  Taxonomy is based on the NCBI taxonomy database.

## How to cite

You can cite this repository directly:  
Teresita M. Porter. (2020, April 3). 12S MitoFish Reference Set For The RDP Classifier (Version v1.0.1). Zenodo. http://doi.org/10.5281/zenodo.4741464    

Please also cite the MitoFish database where the mitodhonrial genome sequences are available:

Sato, Y., Miya, M., Fukunaga, T., Sado, T., Iwasaki, W., Kumar, S. (2018) MitoFish and MiFish Pipeline: A mitochondrial genome database of fish with an analysis pipeline for environmental DNA metabarcoding.  Molecular Biology and Evolution, 35: 1553.

If you use this reference set with the RDP classifier please also cite the naive Bayesian classification tool:

Wang et al. (2007) Naïve Bayesian classifier for rapid assignment of rRNA sequences into the new bacterial taxonomy. Applied and Environmental Microbiology, 73: 5261.

## Quick Start
```linux
############ Install the RDP classifier if you need it
# The easiest way to install the RDP classifier v2.13 is using conda
conda install -c bioconda rdp_classifier
# Alternatively, you can install from SourceForge and run with java if you don't use conda
wget https://sourceforge.net/projects/rdp-classifier/files/rdp-classifier/rdp_classifier_2.13.zip
# decompress it
unzip rdp_classifier_2.13
# record path to classifier.jar ex. /path/to/rdp_classifier_2.13/dist/classifier.jar

############ Get the latest 12S training set
wget https://github.com/terrimporter/12SfishClassifier/releases/download/v1.0/mydata_trained.tar.gz

# decompress it
tar -xvf mydata_trained.tar.gz

# record the path to the rRNAClassifier.properties file ex. /path/to/mydata_trained/rRNAClassifier.properties

############ Run the RDP Classifier 
# If it was installed using conda, run it like this:
rdp_classifier -Xmx8g classify -t /path/to/mydata_trained/rRNAClassifier.properties -o rdp.output query.fasta
# Otherwise run it using java like this:
java -Xmx8g -jar /path/to/rdp_classifier_2.13/classifier.jar -t /path/to/mydata_trained/rRNAClassifier
```

# Releases

### 12S fish v1.0

Created from the MitoFish database [accessed March 16, 2020].  This version contains 2853 reference sequences and 4751 taxa at all ranks.

Fish mitogenomes were obtained from http://mitofish.aori.u-tokyo.ac.jp [March 16/20] and the 12S region was extracted for this custom reference set. 

**Taxonomic assignment results should be filtered according to their bootstrap support values to reduce false positive assignments.**  Cutoffs are based on leave-one-sequence-out testing of non-singleton species. Here we recommend MINIMUM bootstrap cutoffs according to query length and assignment rank.  Assuming your query sequences are represented in the reference set, using the cutoffs presented in the first table below should ensure 99% accuracy.  If you wish to cast a wider net, you can use the second table below for 95% accuracy.

#### Bootstrap support cutoffs, 99% accuracy:

Rank | 500 bp+ | 400 bp | 300 bp | 200 bp | 100 bp
--- |:---:|:---:|:---:|:---:|:---:
Superkingdom | 0 | 0 | 0 | 0 | 0
Kingdom | 0 | 0 | 0 | 0 | 0
Phylum | 0 | 0 | 0 | 0 | 0
Class | 0 | 0 | 0 | 0 | 0
Order | 0.50 | 0.40 | 0.40 | 0.40 | 0.50
Family | 0.95 | 0.95 | 0.90 | 0.80 | 0.90
Genus | NA | NA | NA | NA | NA
Species | NA | NA | NA | NA | NA

NA = No cutoff available will result in 99% correct assignments

#### Bootstrap support cutoffs, 95% accuracy:

Rank | Full | 400 bp | 300 bp | 200 bp | 100 bp
--- |:---:|:---:|:---:|:---:|:---:
Superkingdom | 0 | 0 | 0 | 0 | 0
Kingdom | 0 | 0 | 0 | 0 | 0
Phylum | 0 | 0 | 0 | 0 | 0
Class | 0 | 0 | 0 | 0 | 0
Order | 0 | 0 | 0 | 0.10 | 0.30
Family | 0.10 | 0.20 | 0.20 | 0.20 | 0.30
Genus | NA | NA | NA | NA | NA
Species * | NA | NA | NA | NA | NA

* Leave one sequence out testing (LOOT) is unreliable at this rank because most species are only represented by a single reference sequence.  LOOT testing is only conducted on non-singleton taxa.
NA = No cutoff available will result in 95% correct assignments

#### Bootstrap support cutoffs, 90% accuracy:

Rank | Full | 400 bp | 300 bp | 200 bp | 100 bp
--- |:---:|:---:|:---:|:---:|:---:
Superkingdom | 0 | 0 | 0 | 0 | 0
Kingdom | 0 | 0 | 0 | 0 | 0
Phylum | 0 | 0 | 0 | 0 | 0
Class | 0 | 0 | 0 | 0 | 0
Order | 0 | 0 | 0 | 0 | 0
Family | 0 | 0 | 0 | 0 | 0.20
Genus | 0.80 | 0.80 | 0.80 | 0.70 | 0.80
Species * | NA | NA | NA | NA | NA

* Leave one sequence out testing (LOSO) is unreliable at this rank because most species are only represented by a single reference sequence.  LOSO testing is only conducted on non-singleton taxa.
NA = No cutoff available will result in 90% correct assignments

# References

Sato, Y., Miya, M., Fukunaga, T., Sado, T., Iwasaki, W., Kumar, S. (2018) MitoFish and MiFish Pipeline: A mitochondrial genome database of fish with an analysis pipeline for environmental DNA metabarcoding.  Molecular Biology and Evolution, 35: 1553. Available from http://mitofish.aori.u-tokyo.ac.jp/

Wang, Q., Garrity, G. M., Tiedje, J. M., & Cole, J. R. (2007). Naive Bayesian Classifier for Rapid Assignment of rRNA Sequences into the New Bacterial Taxonomy. Applied and Environmental Microbiology, 73(16), 5261–5267. Available from https://sourceforge.net/projects/rdp-classifier/

# Acknowledgements

We acknowledge support from the Canadian federal Genomics Research & Development Initiative (GRDI), Metagenomics-Based Ecosystem Biomonitoring (Ecobiomics) project.

Last updated: July 19, 2022
