# modules-4-GenePattern
modules for integrating under GenePattern some extra tools for NGS analysis

Usage : upload the zip files in your GenePattern server via the "Modules & Pipelines"/"Install From Zip" menu. For many of the modules you will have to install the software package itself since the module only provides an interface but does not contain the actual tool (see the list below).

There are some changes you might wish to do :
* Some modules contain one or more selectors that allow to choose genome related data like genomic sequences, GTF files with genome annotations, indexed genomes for mapping, etc. By default they point to the anonymous ftp server of the VIB BioinformaticsCore in Ghent (Belgium) and of course contain the genomes of interest for the laboratories affiliated with the VIB. You might wish to point instead to an anonymous ftp server with data that are more relevant for you and eventually one you maintain yourself. You then must unzip the archive, in the "manifest" file replace choiceDir=ftp\://193.191.128.4/pub" by whatever is appropriate, re-zip the archive and upload.
* Some software tools support multithreading. In this case the module will contain a wrapper file XXX_wrapper.pl with a line  
$Nthreads = 4;  
You can, if desirable, replace the 4 by whatever you find appropriate. You can apply this change in the zip file before uploading or you can do it after uploading in the taskLib folder of GP.

# List of modules
* **BCFtools.Call_variants**  
uses BCFtools to compare mapped reads to a reference genome and call variants  
You need to download samtools-1.6.tar.bz2 and bcftools-1.6.tar.bz2 from http://www.htslib.org, deploy them in the patches folder of GP and compile.
* **BgzipAndTabixindex**  
**TabixSearch**  
facility to index and search files with read mappings or genome annotations  
You need to download tabix-0.2.6.tar.bz2 from http://samtools.sourceforge.net, deploy it in the patches folder of GP and compile.
* **BWA.mem**  
interface to the BWA read to genome mapper, suited for mapping long reads used for variant analysis  
You need to download bwa-0.7.15.tar.bz2 from http://bio-bwa.sourceforge.net, deploy it in the patches folder of GP and compile.
* **DeTar**  
**UnZip**  
simple facilities to extract the data from a compressed archive or file, useful as part of a data analysis pipeline
* **STAR.aligner**  
**STAR.indexer**  
interface to the STAR RNA-seq read to genome mapper. 
You need to download STAR-2.5.2a.tar.gz or STAR-2.5.2b.tar.gz from http://github.com/alexdobin/STAR and deploy it in the patches folder of GP.
