#Perl Homework 1
##Problem 1A: Processing a FASTQ file
Download the example fastq file in this directory: https://github.com/NGSAnalysisOnBeocatClass/homework/blob/master/SRR014849_1_short.fastq

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

The second line is the actual sequence read off of the machine.

The third line will have a '+' sign. It is not used at the moment, so ignore it, but the '+' does need to be present for most fastq files to validate.

The fourth line is an sequence of characters that represents the quality of each base of the sequence on line 2. The illumina tech support document describes this in detail.

Fasta files, while named similarly, in practice are much different than fastq files. Moreover, the format of Fasta files varies considerably. For the moment, you should generate an unjustified fasta file. The first line is the sequence identifier starting with a '>' character, and the next line is the sequence itself. Thus, the above Fastq sequence is as follows in fasta format. NOTE! the '@' character has been substititued for the '>'.
```
>SRR014849.2 EIXKN4201AKDUH/2
TCAAGTGGTGAACGGCAGAAA
```

####Start by writing a script that can input a fastq file, and print it back out. 

Some tidbits that can help you.

To get a file name from a user
```perl
my $filename = <STDIN>;
```
To open a file for reading
```perl
open(FILEHANDLE, '<', "<$filename");
```

To read over every line of a file, line-by-line
```perl
while(<FILEHANDLE>)
{
  #do something
}
```

###Now that you can read the Fastq file, next add code that identify lines with a sequence header, and print them back out, ignoring everything else.

You can find text as follows
```perl
if (m/^@/)
{
  #do something
}
```
This tells perl to match text starting with an '@' character. This is important, because illumina quality lines can have the '@' character in them, so we need to specifically look for characters at the start of the line. This is not all, because quality lines can *start* with an '@' character, you need to add additional code to keep track of where you are at in the the file. Since a fastq file repeats every 4 lines, this requires nexting your if statement blocks

To be complete, let's go over the regular expresion up there. Perl can do search and replace using constructs called regular expressions. These often look like gobbledegoook, but once you understand them, they are extremely fast and powerful ways fo analyzing text. In the if statement above, the regex
```perl
m/^@/
```
Tells perl to "match" any string starting with an '@'. Everything between the '/' and '/' is a directive to perl on what to look for. Like find "find" in MS Word. You can also substitute text, using 
```perl
s/^@/>/
```
This tells perl to first fine strings staring with a '@' character, and then replace them with the text between the next '/' and '/', of with a '>' character. You can use substitutions and matching withing if statements. Like double quoted string literals, perl also can match using special characters and variable, so some characters need escaping. We will cover regular expression in more detail later. For now, if perl can make a substitution, it will register true, so you can do the following.
```perl
if (s/^@/>/)
{
  #do something
}
```
Use this, with your knowledge of fastq format files, to print out the headers of the Fastq file in fasta format.

###Finally, add code to print out the sequence on the next line below the header.
Don't forget how newlines are handled, as well as the difference between print and say. Use this to make a fasta file from the fastq file. Don't forget that you can use the unix command line promt to redirect the output of your script with ethe following unix command
```unix
your_perl_script.pl > outfile.txt
```

##Problem 1B: Determine the average read length of your fastq file

Make a new version of the fastq processing script from above. In your new version of the script, instead of printing the file in fasta format, instead let's examine the quality of this fastq file, by printing out useful information. For this excercise, let's print out the average sequence length, and the standard deviation of read length to get an idea of how many, if any, short or long reads are in the file. Use your assignment operators to do this. 

###Output the average sequence length, and standard error of the mean. 

You can find out how to calculate the standard error of the mean here: https://en.wikipedia.org/wiki/Standard_error#Standard_error_of_the_mean.

Finally, one of the most common problems you will face is fastq files that have issues with data quality, or corruption. The following fastq file has problems with it. 
https://github.com/NGSAnalysisOnBeocatClass/homework/blob/master/SRR014849_quality_issues.fastq

###Filter out the reads that are short, or are missing quality information (e.g. quality is shorter than the sequence). Bonus if you can output reads separatrely into a "keeper file" and a separate "problem reads" file.

In addition, there are some very long reads in the file, bonus if you can identify them and print them to their own file.
























