#Perl Homework #2

Genomes are commonly annotated with GFF format files. Unfortunately, the way in which GFF files are implemented is a complete mess that has been exacerbated by having different software tools utilize different flavors of GFF files. In their essence, a GFF file is a listing of gene features. Each line lists features in a genome, such as a "gene", "CDS" and so forth. Currently, there has been considerable effort made in standardizing GFF files, into so called GFF3 format. Older styles of GFF format are called GTF format, of GFF2.5, or GFF2.0 depending on the implementation (it is a complete mess). In essence, GFF3 made considerable strides in stnadardizing the type of data that can go into each column.

A description of the format can be found here:

http://www.sequenceontology.org/gff3.shtml

A simple GFF3 format file for Chlamydomonas (for the first gene on chromosome_1) looks like this

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

Before you get too deep into processing GFF3 and genome files (which are big, but not terribly large) that take a long time to process, it is time to start understanding how to build tests. In order to process most GFF3 files and their corresponding genomes, it will take a few minutes at the very least to slurp the file into memory. If you have to wait even 5 minutes each tiem you want to debug a script, it can take hours just waiting for the file to be slurped into memory. Even worse, there is no way for you to verify that there are no bugs in any calculations you make.

Thus, it is AWLAYS good practice to make a test data set and ensure it is behaving as expected. One of the fastest ways to create a test file, is to utilize the Unix command 'head' that will spit out the first 10 lines of a file. Head has a nice option that allows you to output any number of lines that you are interested in.

For example, this command will output the first 10,000 lines of file.txt to STDOUT.

```unix
head -n 10000 file.txt
```

So you can use the head command to make a subset of your data to run on your scripts as a test. 

If a file is zipped, you can pipe the command 'gunzip' to head. By using 'gunzip -c' this will unzip the zipped file, while preserving the original file. As disk space is always at a premium, it is a good idea to keep your source files zipped, and even read only so you don't screw them up (and make backups!!!). In this case, you could make test files as follows...

```unix
gunzip -c file.gz | head -n 10000 > file.txt
```

This will unzip file.gz in memory, send this unzipped data via a pipeline to the command head, that will output the first 10,000 lines into the file file.txt. Note that this command will overwrite any data in file.txt without warning, so make sure you are careful with your data files. As mentioned above, making source data files read only is a very good practice, and keeping off machine backups is also a good idea. It only take a small coding bug to wipe out the contents of a data file.

In other cases, such as a GFF3 file, you want to make sure that your data, which is on multiple, but variable numbers of lines, is a complete set of GFF3 lines. In this case, often you will have to make a custom perl script to building testing file, before you even start coding your actual analysis script.

Also, don't forget that you can supply a file name to process as a command line argument. This is often easier than dealing with STDIO to input a filename as you can use the bash shell to autocompelte the file name.

```perl
my $filename=$ARGV[0];
open(FILE, '<', $filename);

#do something with file
close file;
```


Download the Chlamydomonas genome, and corresponding GFF3 files from KSOL.

###2A: First, build a perl script to output the first 10 gene annotations from the file into a new testing GFF3 file. Call the file Chlamy_test.gff3 or whatever works for you.

###2B: Next, build a perl script to output only the sequnce for chromsome_1 from the fasta file into a new file. Note that the Chlamydomonas genome is a "justified" fasta file, which can be a bit of a challenge to process correctly. Call this file Chlamy_chr1.fa.

Using your test files for debugging, build a perl script that can tell you some useful things about the Chlamydomonas genome. When your scripts work with your test files, run them on the entire Chlamydomonas genome.

In order to deal with tab separated data in perl, you want to use one the 'split' function. Here is a really complete tutorial, http://www.perlmonks.org/?node_id=591988, however, for the moment you can do a lot with split without knowing much about regular expressions. Split uses the syntax of..
```perl
my @array=split(/\t/, $some_string);
```
The split funciton takes a regular expression, in this case delimited with / and /, and splits a sclar into elements of an array everytime the regular expression matches in the scalars. In the code above, split will break up $some_string into array elements every time there is a tab and assign all those elements sequentially into the array @array. Thus, you can take in a line from a file, split it up into array element without having to know anything about the length of the data.

NOTE!! It is possible to introduce bugs into your script if you forget to chomp the incoming line, especially if you expect numbers to be the last element of the incoming line and try and do calculations on those number.

For future reference, split can also work to split strings up into arrays of the individual characters in the string. This comes in handy when you want to process DNA or RNA sequence data and want to do fast comparisons on a base-by-base basis. In fact, using just a little bit of code, splitting a string into characters into an array is a very fast way to identify SNPs in a data set compared to a reference. It is also a fast way to reduce your comparison to just the differences between two string values. This is very handy when you have genome sized DNA fragments and only want to look at the differences between two sequences. Here is an example.
```perl
#!/usr/bin/perl
use strict;
use warnings;
use 5.010;

#Two test DNA sequences
my $dna1='ATCG';
my $dna2='AACG';

#Now turn sequences into arrays
#Split based on a null string delimited with // as a regular expression
my @dna_array1=split(//, $dna1);
my @dna_array2=split(//, $dna2);

#Let's start by printing a header
say "Here are the differences between the sequences";
say "DNA1\tDNA2\tPosition";

#First lets ensure that the DNA sequences are the same length
#This is a god sanity check before processing lots of data
#Especially since the for loop below processes the arrays in parallel
if(scalar(@dna_array1) == scalar(@dna_array2))
{
  #If the lengths are the same look for SNPs
  for (my $i=0; $i<=$#dna_array1; $i++)
  {
    #Now we are going to test if the element in each position of the two arrays is the same
    #Note that we are comparing string data, so we use ne
    #When you learn about hashes, you could store all this data in a hash for later processing
    if($dna_array1[$i] ne $dna_array2[$i])
    {
      say "$dna_array1[$i]\t$dna_array2[$i]\t$i"; 
    }
  }
}
else #If the sequences are unequal in length
{
  say "The DNA sequences are different lengths!";
}
```




###2C: Build a acript that outputs the following data about the Chlamydomonas genome. 1) Number of genes, 2) Average length of a gene. 3) Number of genes on the '+' strand, and on the '-' strand, 4) Number of geens on chromosomes, versus scaffolds, 5) Average number of genes per chromosome.

###2D: Now add onto your script to process the chlamydomonas fasta genome file to calculate gene density. You will probably want to use subroutines!

Once you get this going, lets do some advanced calculations.

###2D: Output the following calculated data 1) average intron length, 2) number of genes in the following orientation ----> <---- versus <----- ----> versus -----> ------> (same as <---- <----), and the average size between these sequences in this orentation.

As a reminder, if you try and do this on the full genome data you will be waiting forever to get your software running. You will need to check the math of your work in your test files as well. For problem 2D, you will need to make a test GFF3 file for all of chromosome_1.

You will need to get these scripts running because on Monday, you will build on these scripts to use hashes to export CDS and gene sequences. Thus, make sure you are compartmentalizing code in sub routines whenever possible. Use arrays to store data for GFF3 file for easy acceess. Also do not forget your assignment operators such as '+=' and '.+'.









