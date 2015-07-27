#Perl Homework 1
##Problem 1A: Processing a FASTQ file
Download the example fastq file: here

Fastq formatted files repeat every 4 lines. 
```
@SRR014849.2 EIXKN4201AKDUH/2
TCAAGTGGTGAACGGCAGAAA
+
<=B:==B:=<?6=B;<;=B=)
```

The first line starting with "@" is the sequence identifer. These vary considerably between instruments, see below for how current versions of Illumina instruments handle these headers


Illumina provides a support document that describes the Fastq format in significant detail.
http://support.illumina.com/help/SequencingAnalysisWorkflow/Content/Vault/Informatics/Sequencing_Analysis/CASAVA/swSEQ_mCA_FASTQFiles.htm


