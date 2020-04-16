# modules-4-GenePattern
modules for integrating under GenePattern some extra tools for NGS analysis

Usage : upload the zip files in your GenePattern server via the "Modules & Pipelines"/"Install From Zip" menu. For many of the modules you will have to install the software package itself since the module only provides an interface but does not contain the actual tool (see the list below). Note that the current versions of the modules do not rely on dockers and have only been used routinely with GenePattern version 3.9.10. Making them work under newer versions might demand some tweeking.

There are some changes you might wish to do :
* Some modules contain one or more selectors that allow to choose genome related data like genomic sequences, GTF files with genome annotations, indexed genomes for mapping, etc. By default they point to the anonymous ftp server of the VIB BioinformaticsCore in Ghent (Belgium) and of course contain the genomes of interest for the laboratories affiliated with the VIB. You might wish to point instead to an anonymous ftp server with data that are more relevant for you and eventually one you maintain yourself. You then must unzip the archive, in the "manifest" file replace "choiceDir=ftp\://data.gp.vib.be/pub" by whatever is appropriate, re-zip the archive and upload.
* Some software tools support multithreading. In this case the module will contain a wrapper file XXX_wrapper.pl with a line  
$Nthreads = 4;  
You can, if desirable, replace the 4 by whatever you find appropriate. You can apply this change in the zip file before uploading or you can do it after uploading in the taskLib folder of GP.

# List of modules
* **BCFtools.Call_variants**  
uses BCFtools to compare mapped reads to a reference genome and call variants  
You need to download bcftools-1.9.tar.bz2 from http://www.htslib.org, deploy it in the patches folder of GP and compile.
* **BgzipAndTabixindex**  
**TabixSearch**  
facility to index and search files with read mappings or genome annotations  
You need to download htslib-1.9.tar.bz2 from http://www.htslib.org, deploy it in the patches folder of GP and compile.
* **BWA.mem**  
interface to the BWA read to genome mapper, suited for mapping long reads used for variant analysis  
You need to download bwa-0.7.17.tar.bz2 from http://bio-bwa.sourceforge.net, deploy it in the patches folder of GP and compile.
* **DeTar**  
**UnZip**  
simple facilities to extract the data from a compressed archive or file, useful as part of a data analysis pipeline
* **FastQC**  
noninteractive-interface to the FastQC tool for testing the quality of sequencing reads  
You need to download fastqc_v0.11.8.zip from http://www.bioinformatics.babraham.ac.uk/projects/fastqc and deploy it in the patches folder of GP ; make sure .../patches/FastQC/fastqc is executable by the user that runs GP.
* **GtfToBed**  
simple facility to convert a GTF file into a 12-column BED file suitable as input to the RSeQC suite
* **HTSeq.Count**  
interface to the HTseq RNA-seq mapped read counter  
The simplest is to install it with the command :  
pip3 install htseq==0.11.1  
Otherwise, go to http://htseq.readthedocs.io and follow the instructions. Note that you need Python version 3.4 or higher. You also must in the genepattern.resources file of your GP add a line like :  
HTSEQ=/usr/bin/htseq-count  
and restart the server.
* **Kallisto.aligner**  
**Kallisto.indexer**  
**Kallisto.SingleCell2BUS**  
interface to the Kallisto RNA-seq read to transcriptome mapper  
You need to download kallisto_linux-v0.46.0.tar.gz from https://pachterlab.github.io/kallisto and deploy it in the patches folder of GP.
* **Picard.BuildBamIndex**  
**Picard.CollectAlignmentSummaryMetrics**  
**Picard.CollectMultipleMetrics**  
**Picard.MarkDuplicates**  
**Picard.SortSam**  
interface to some tools of the Picard suite for SAM/BAM file analysis and manipulation (tools not available or not so up-to-date in the standard GP distribution)  
You need to download picard.jar (version 2.21.1) from http://broadinstitute.github.io/picard and put it in the patches folder of GP, preferably in a subfolder picard_2.21.1.  
To profit from the graphical output you need R with support for PNG and JPEG graphics.
* **Qualimap.BamQC**  
**Qualimap.MultisampleBamQC**  
**Qualimap.RnaSeqQC**  
noninteractive-interface to the Qualimap tool for testing the quality of mapping data in BAM format  
You need to download qualimap_v2.2.1.zip from http://qualimap.bioinfo.cipf.es and deploy it in the patches folder of GP. You might have to edit the qualimap master script. In the line :  
java_options="-Xms32m ....  
add :
java_options="-Djava.awt.headless=true -Xms32m ....  
to avoid Qualimap trying to open a graphical window, if it cannot. Also you might have to increase available memory by modifying :  
JAVA_MEM_DEFAULT_SIZE="1200M"
* **RSeQC.BamStat**  
**RSeQC.GeneBodyCoverage**  
**RSeQC.InferExperiment**  
**RSeQC.InnerDistance**  
**RSeQC.JunctionAnnotation**  
**RSeQC.JunctionSaturation**  
**RSeQC.ReadDistribution**  
**RSeQC.ReadDuplication**  
interface to some tools of the RSeQC suite for testing the quality of mapping data in SAM/BAM format  
The simplest is to install it with the command :  
pip3 install RSeQC==3.0.1  
Otherwise, go to http://rseqc.sourceforge.net and follow the instructions. Note that you need Python version 3.4 or higher. You also must in the genepattern.resources file of your GP add a line like :  
RSEQC=/usr/bin  
and restart the server.  
To profit from the graphical output you need R with support for PNG and JPEG graphics.
* **Samtools.SamView**  
an interface to a tool from the Samtools suite, allows to extract data from a SAM/BAM file in a variety of ways  
You need to download samtools-1.9.tar.bz2 from http://www.htslib.org, deploy it in the patches folder of GP and compile.
* **STAR.aligner**  
**STAR.indexer**  
interface to the STAR RNA-seq read to genome mapper. 
You need to download STAR-master.zip from http://github.com/alexdobin/STAR and deploy it in the patches folder of GP.
* **VarScan**  
**VarScan.Cancer**  
**VarScan.Trio**  
interface to the VarScan suite to compare mappings to a reference genome and call variants  
You need to download VarScan.v2.4.4.jar from http://dkoboldt.github.io/varscan and put it in the patches folder of GP. You also need to download samtools-1.9.tar.bz2 from http://www.htslib.org, deploy in the patches folder of GP and compile.
* **VCF_compare**  
**VCF_intersect** 
interface to some tools from the VCFtools suite for VCF file analysis and manipulation, to find what variants VCF files have in common
You need to download vcftools-vcftools-v0.1.16-16-g954e607.tar.gz from http://vcftools.github.io, deploy it in the patches folder of GP and compile (follow the instructions in the included README.md file). You also need to download htslib-1.9.tar.bz2 from http://www.htslib.org, deploy it in the patches folder of GP and compile.  
For VCF_compare to work you need R with support for PNG and JPEG graphics, and you must install the library "colorfulVennPlot".
