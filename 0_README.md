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
* **FastQC**  
noninteractive-interface to the FastQC tool for testing the quality of sequencing reads  
You need to download fastqc_v0.11.7.zip from http://www.bioinformatics.babraham.ac.uk/projects/fastqc and deploy it in the patches folder of GP ; make sure .../patches/FastQC/fastqc is executable by the user that runs GP.
* **GtfToBed**  
simple facility to convert a GTF file into a BED file suitable as input to the RSeQC suite
* **HTSeq.Count**  
interface to the HTseq RNA-seq mapped read counter  
You need to download HTSeq-0.9.1.tar.gz from http://htseq.readthedocs.io and follow the instructions on the site for how to install the auxilary libraries and install HTSeq in your Python installation.
* **Kallisto.aligner**  
**Kallisto.indexer**  
interface to the Kallisto RNA-seq read to transcriptome aligner  
You need to download kallisto_linux-v0.43.1.tar.gz from https://pachterlab.github.io/kallisto and deploy it in the patches folder of GP.
* **Picard.CollectMultipleMetrics**  
**Picard.MarkDuplicates**  
**Picard.SortSam**  
interface to some tools of the Picard suite for SAM/BAM file analysis and manipulation (tools not available or not so up-to-date in the standard GP distribution)  
You need to download picard.jar (version 2.10.10) from http://broadinstitute.github.io/picard and put it in the patches folder of GP, preferably in a subfolder picard_2.10.10.
* **Qualimap.BamQC**  
**Qualimap.MultisampleBamQC**  
noninteractive-interface to the Qualimap tool for testing the quality of mapping data in BAM format  
You need to download qualimap_v2.2.1.zip from http://qualimap.bioinfo.cipf.es and deploy it in the patches folder of GP.
* **RSeQC.BamStat**  
**RSeQC.GeneBodyCoverage**  
**RSeQC.InferExperiment**  
**RSeQC.InnerDistance**  
**RSeQC.JunctionSaturation**  
**RSeQC.ReadDistribution**  
**RSeQC.ReadDuplication**  
interface to some tools of the RSeQC suite for testing the quality of mapping data in SAM/BAM format  
You can install it with the command :  
pip install RSeQC  
You must add to the resources/genepattern.properties file of your GP a line  
RSEQC=/usr/bin  
and restart the server.  
To profit from the graphical output you need R with support for PNG and JPEG graphics.
* **Samtools.SamView**  
an interface to a tool from the Samtools suite, allows to extract data from a SAM/BAM file in a variety of ways  
You need to download samtools-1.6.tar.bz2 from http://www.htslib.org, deploy it in the patches folder of GP and compile.
* **STAR.aligner**  
**STAR.indexer**  
interface to the STAR RNA-seq read to genome mapper. 
You need to download STAR-2.5.2a.tar.gz or STAR-2.5.2b.tar.gz from http://github.com/alexdobin/STAR and deploy it in the patches folder of GP.
* **VarScan**  
**VarScan.Cancer**  
**VarScan.Trio**  
interface to the VarScan suite to compare mappings to a reference genome and call vaiants  
You need to download VarScan.v2.4.3.jar from http://dkoboldt.github.io/varscan and put it in the patches folder of GP. You also need to download samtools-1.6.tar.bz2 and bcftools-1.6.tar.bz2 from http://www.htslib.org, deploy them in the patches folder of GP and compile.
* **VCF_intersect**  
an interface to a tool from the VCFtools suite for VCF file analysis and manipulation, finds the interscetion between two VCF files  
You need to download vcftools-vcftools-v0.1.15-5-gea875e2.tar.gz from http://vcftools.github.io, deploy it in the patches folder of GP and compile (follow the instructions in the included README.md file). You need also to download tabix-0.2.6.tar.bz2 from http://samtools.sourceforge.net, deploy it in the patches folder of GP and compile.
