#Perl Homework #2

Genomes are commonly annotated with GFF format files. Unfortunately, the way in which GFF files are implemented is a complete mess that has been exacerbated by having different software tools utilize different flavors of GFF files. In their essence, a GFF file is a listing of gene features. Each line lists features in a genome, such as a "gene", "CDS" and so forth. Currently, there has been considerable effort made in standardizing GFF files, into so called GFF3 format. Older styles of GFF format are called GTF format, of GFF2.5, or GFF2.0 depending on the implementation (it is a complete mess). In essence, GFF3 made considerable strides in stnadardizing the type of data that can go into each column.

A description of the format can be found here:

http://www.sequenceontology.org/gff3.shtml

A simple GFF3 format file for Chlamydomonas looks like this

```GFF3
##gff-version 3
chromosome_1	phytozome8_0	gene	24026	30617	.	+	.	ID=Cre01.g000050;Name=Cre01.g000050
chromosome_1	phytozome8_0	mRNA	24026	30617	.	+	.	ID=PAC:26903339;Name=Cre01.g000050.t1.3;pacid=26903339;longest=1;geneName=RWP14;Parent=Cre01.g000050
chromosome_1	phytozome8_0	exon	24026	28105	.	+	.	ID=PAC:26903339.exon.1;Parent=PAC:26903339;pacid=26903339
chromosome_1	phytozome8_0	five_prime_UTR	24026	24125	.	+	.	ID=PAC:26903339.five_prime_UTR.1;Parent=PAC:26903339;pacid=26903339
chromosome_1	phytozome8_0	CDS	24126	28105	.	+	0	ID=PAC:26903339.CDS.1;Parent=PAC:26903339;pacid=26903339
chromosome_1	phytozome8_0	exon	28291	28644	.	+	.	ID=PAC:26903339.exon.2;Parent=PAC:26903339;pacid=26903339
chromosome_1	phytozome8_0	CDS	28291	28644	.	+	1	ID=PAC:26903339.CDS.2;Parent=PAC:26903339;pacid=26903339
chromosome_1	phytozome8_0	exon	28842	29091	.	+	.	ID=PAC:26903339.exon.3;Parent=PAC:26903339;pacid=26903339
chromosome_1	phytozome8_0	CDS	28842	29091	.	+	1	ID=PAC:26903339.CDS.3;Parent=PAC:26903339;pacid=26903339
chromosome_1	phytozome8_0	exon	29347	30617	.	+	.	ID=PAC:26903339.exon.4;Parent=PAC:26903339;pacid=26903339
chromosome_1	phytozome8_0	CDS	29347	29577	.	+	0	ID=PAC:26903339.CDS.4;Parent=PAC:26903339;pacid=26903339
chromosome_1	phytozome8_0	three_prime_UTR	29578	30617	.	+	.	ID=PAC:26903339.three_prime_UTR.1;Parent=PAC:26903339;pacid=26903339
chromosome_1	phytozome8_0	gene	30776	41037	.	+	.	ID=Cre01.g000100;Name=Cre01.g000100
```
