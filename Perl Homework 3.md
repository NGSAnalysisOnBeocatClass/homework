#Homework 3
In this excercise you will solve two problems that are best approached with hashes.

For your first challenge, use hashes to develop a program that translates a CDS sequence into its predicted amino acid sequence. As always start with test data first and get your program working. For this example using subroutines will make your life much easier.

###Problem #1A: Write code that will translate a DNA sequence into a protein sequence

###Problem #1B: Using code bases you have build, write a program that takes as it input, a fasta file with DNA sequences, then translates the sequences into proteins in fasta format. Below is a sample fasta file.

```
>gi|8752025|gb|BE208627.1|BE208627 ba13f12.y1 NIH_MGC_7 Homo sapiens cDNA clone IMAGE:2824271 5' similar to gb:K00558 TUBULIN ALPHA-1 CHAIN (HUMAN); gb:M13446 Mouse alpha-tubulin isotype M-alpha-2 mRNA, complete cds (MOUSE);, mRNA sequence
CGACTCTTAGCTTGTCTGGGACGGTAACCGGGACCCGGTGTCTGCTCCTGTCGCCTTCGCCTCCTAATCC
CTAGCCACTATGCGTGAGTGCATCTCCATCCACGTTGGCCAGGCTGGTGTCCAGATTGGCAATGCCTGCT
GGGAGCTCTACTGCCTGGAACACGGCATCCAGCCCGATGGCCAGATGCCAAGTGACAAGACCATTGGGGG
AGGAGATGACTCCTTCAACACCTTCTTCAGTGAGACGGGCGCTGGCAAGCACGTGCCCCGGGCTGTGTTT
GTAGACTTGGAACCCACAGTCATTGATGAAGTTCGCACTGGCACCTACCGCCAGCTCTTCCACCCTGAGC
AGCTCATCACAGGCAAGGAAGATGCTGCCAATAACTATGCCCGAGGGCACTACACCATTGGCAAGGAGAT
CATTGACCTTGTGTTGGACCGAATTCGCAAGCTGGCTGACCAGTGCACCGGTCTTCAGGGCTTCTTGGGT
TTCCACAGCTTTGGTGGGGGAACTGGTTCTGGGTTCACCTCCCTGCTCATGGAACGTCTCTCAGTTGATT
ATGGCAAGATATCCAAGCTGGAGTTTTCCATTTACCCGGCACCCCAGGTTTCCACAGCTGTAGGTGAGAC
CTACAAC

>gi|8752055|gb|BE208657.1|BE208657 ba67g10.x1 NIH_MGC_20 Homo sapiens cDNA clone IMAGE:2905506 3' similar to gb:K00558 TUBULIN ALPHA-1 CHAIN (HUMAN); gb:M13441 Mouse alpha-tubulin isotype M-alpha-6 mRNA, complete cds (MOUSE);, mRNA sequence
TTAAAATGGAAACATCAATTTTATTAACAATTTACGGCAATAGACATTTACAGAACAAAAATAAGACAGT
TCCAAGACAAAGGAGTGTAAAAGTACAGCACACAGGTTAATACTCTTCACCCTCATCCTCTCCGTCAGCA
CTATCTGCTCCAACCTCCTCATAATCCTTCTCAAGGGCAGCCATGTCCTCACGGGCCTCTGAAAACTCGC
CTTCCTCCATCCCCTCACCCACGTACCAGTGAACAAAGGCACGCTTGGCATACATCAGGTCAAACTTGTG
GTCCAGGCGAGCCCAGACCTCGGAAACAGCTGTGGTATTGCTCATCATGCACACAGTTTCTCTGTACCTT

>gi|8749675|gb|BE206277.1|BE206277 bb57b01.x1 NIH_MGC_17 Homo sapiens cDNA clone IMAGE:3010729 3' similar to gb:K00558 TUBULIN ALPHA-1 CHAIN (HUMAN); gb:M13444 Mouse alpha-tubulin isotype M-alpha-4 mRNA, complete cds (MOUSE);, mRNA sequence
TTTTTTTTTTTTTTGCAAGGAAACTGTTTTTTTCGAAAGGATTTTGCATTAAACATAGTGAATAGGCTCC
AGGCAGCTGCTTTATTCTTTTCCCTCATCCTCGTCCTCATTTGAGTCGATGCCCACCTCCTCATAATCCT
TCTCCAGGGCAGCCATATCCTCACGGGCCTTGGAGAACTCACCCTCCTCCATGCCCTCACCCACATACCA
GTGCACAAACGCCCTCTTGGCATACATCAGGTCGAACTTGTGGTCCAGGCGGGCCCAGGCCTCGGCGATG
GCGGTCGTGTTGCTCATCATGCACACGGCACGCTGCACCTTGGCCAGGTCACCCCCAGGCACCACAGTGG
GAGGCTGGTTGTTGTTACCAACCTTGAAGCCTGTGGGGCACCTGTCCACAAACTGAATGCTGCGCTTGGT
CTTGATGGCGGCAATGGCTGCTTTGTCATCCTTGGGCCCCCCCTCTCCACGGTACAACA
```

##Problem 2

For this problem, we are going to use hashes to process  a GFF3 formatted file. Again, you must have test files for development, as processing an entire genomes worth of GFF data will take quite a bit of time. We will use the Chlamydomonas GFF3 file, and corresponding Chromosome_1 fasta file.

Now that we are getting into advanced analysis, it is time to figure out how to learn about new Perl functions. One way is perldoc, and another is simply google. Try and find a Perl function that will extract a substring. you will need it for this problem, and more importantly, implement it correctly.

You will start by building on your codebase from the previous homework. Instead of simply pulling data in and storing it in arrays, now let's store the data in a hash, and see how much easier it is than arrays. In your first problem, process only the CDS features for a gene, and store the CDS sequence into a hash. For your first problem, process a gene that is on the '+' start.

###Problem 2A: Read in a GFF test file with a feature on the + strand and extract its CDS sequence. Print the CDS sequence and its translation. If you mess up, the translation will be wrong.

Ok, that seemed easy, but was a lot of work right?

###Problem 2B: Now modify the above code to extract the CDS of a feature on the '-' strand, and print out its translation. Be very careful for the fact that perl counts by 'zero'!!

##Problem 3: Complex data structures introduction

For this, again we are goig to start the process of learning to advance our perl knowledge on our own. Work through as much of this as you can, this will get us moving toward our final project

Read this article from "Programming Perl", the perl book that comes after "Learning Perl".

http://archive.oreilly.com/pub/a/perl/excerpts/9780596000271/data-structures.html

It is an old version, but has everything we need. Work through the code examples in the article.

###Using a hash-of-hash of array to process a single GFF3 entry and hash up all the sub-parts of a gene.

Your complex data structure should look like this:

```perl
geneID  => CDS =>   (gff_line1, gff_line2...)
          five_prime_utr  =>  gff_line
          three_prime_utr =>  gff_line
          ...
```
For every gene you will have a key in a hash, its values will be the GFF parts (CDS, gene, utr etc.). For those parts that that have a single entry (e.g. utr), just store the line from the gff file as a scalar value of the value - a hash-of-hash.

CDS entries are more difficult. Here the value CDS will be used as a key that points to an array of all the gff_lines, not a scalar.







