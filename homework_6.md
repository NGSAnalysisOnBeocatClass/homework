##Homework 6

This assignment was adapted from Rosalind http://rosalind.info/. Rosalind is a great training tool. It describes Python code but you can do each exercise in any language and then test it using their datasets.

In DNA strings, symbols 'A' and 'T' are complements of each other, as are 'C' and 'G'.

The reverse complement of a DNA string **s** is the string **s<sup>c</sup>** formed by reversing the symbols of **s**, then taking the complement of each symbol (e.g., the reverse complement of "GTCA" is "TGAC").

##For this assignment:

1) Create a hash where the keys are the uppercase nucleotide and lowercase nucleotides and the values are the corresponding upper or lowercase complements.

2) open the fasta file passed as the first argument to your perl script for reading. Name the file `$file` when you read `$ARGV[0]`;

3) Parse the filename of the fasta file using the `fileparse` function from the Perl module `File::Basename`. `fileparse` is similar to `basename` in Bash. It takes a filename and an extension as arguments but it outputs an array with the basename, directory, and extension as array elements.

The following two lines can allow you to create variables from the parts of an input filename. This assumes you named `$ARGV[0]` `$file`. Otherwise change `$file` to the correct variable for your input filename. You can use these to create output filenames based on the input filename:

```
use File::Basename; # enable maipulating of the full path
my ($basename, $directories, $suffix) = fileparse($file,'\..*'); # break appart filenames
```

Now you can create a new output filename from the original filename:

```
my $outfile = "${directories}/${basename}_revcomp${suffix}";
```

Create an output filename with `_revcomp` added to the basename using `fileparse`.

4) Open your output file with write permissions ( using `>` instead of `<`)

5) While there are lines to read in your input fasta file: 

-for headers lines print them to the output

-for sequence lines reverse complement them using `split` for the sequence line then `reverse` on the array of bases and use your hash to take the current base as the key and print it's complement to the output file (if the base is ambiguous print it as-is without complementing)


**Remember to add a newline character back to the end of a sequence line**


Sample Dataset

```
>seq1
AAAACCCGGT
```

Sample Output

```
>seq2
ACCGGGTTTT
```
