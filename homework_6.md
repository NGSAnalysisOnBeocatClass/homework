##Homework 6

This assignment was adapted from Rosalind http://rosalind.info/. Rosalind is a great training tool. It describes Python code but you can do each exercise in any language and then test it using their datasets.

In DNA strings, symbols 'A' and 'T' are complements of each other, as are 'C' and 'G'.

The reverse complement of a DNA string **s** is the string **s<sup>c</sup>** formed by reversing the symbols of **s**, then taking the complement of each symbol (e.g., the reverse complement of "GTCA" is "TGAC").

##For this assignment:

Create and edit a file named `rev_comp.pl`.

####Step 1: Reverse complement subroutine

Create a subroutine called `reverse_comp`.

Within the subroutine:

Create a hash where the keys are the uppercase nucleotide and lowercase nucleotides and the values are the corresponding upper or lowercase complements. 

The subroutine should take a string of DNA sequence as the argument `$_[0]`. Within the subroutine:

-- Define `$contig` as `$_[0]`.

-- Create a new variable called `$new_contig`.

-- Reverse `$contig` and add its bases to an array using the `split` then `reverse` functions in Perl to create an array of reversed bases called `@seq` (google "perl split" or "perl reverse array" or look again at your reading in the Perl text for a refresher)

-- Loop through `@seq` using your hash to take the current base as the key and concatenate it's complement to `$new_contig` (if the base is ambiguous (not upper or lowercase A, C, G or T concatenate it as-is without complementing)

When the loop is finished return `$new_contig`

####Step 2: Open your input file

Open the fasta file passed as the first argument to your perl script for reading. Name the file `$file` when you read `$ARGV[0]`;

####Step 3: Create your output file

Parse the filename of the fasta file using the `fileparse` function from the Perl module `File::Basename`. `fileparse` is similar to `basename` in Bash. It takes a filename and an extension as arguments but it outputs an array with the basename, directory, and extension as array elements.

The following two lines can allow you to create variables from the parts of an input filename. This assumes you named `$ARGV[0]` `$file`. Otherwise change `$file` to the correct variable for your input filename. You can use these to create output filenames based on the input filename:

```
use File::Basename; # enable maipulating of the full path
my ($basename, $directories, $suffix) = fileparse($file,'\..*'); # break appart filenames
```

Now you can create a new output filename from the original filename:

```
my $outfile = "${directories}${basename}_revcomp${suffix}";
```

To redirect this output to your working directory `output` you would write:

```
my $outfile = "output/${basename}_revcomp${suffix}";
```

Create an output filename with that begins with the directory `output/` and has `_revcomp` added to the basename using `fileparse`.

####Step 4: Open your output file

Open your output file with write permissions ( using `>` instead of `<`)

####Step 5: Define a new variable

Declare the variable `$current_contig` but do not define it

####Step 6: Parse your input file

While there are lines to read in your input fasta file: 

-- If a line is a header and `$current_contig` is defined (remember for the first line `$current_contig` is undefined for the first header) then run `&reverse_comp` with the argument `$current_contig`. Print the return from `&reverse_comp` and a new line character to the output file. Then print `$_`. Whether or not the header is the first print the header `$_` to the output file.

-- If the line is not a header (i.e. it is sequence data) remove newline characters and concatinate the line to `$current_contig`

-- If the line is the end of the file run `&reverse_comp` with the argument `$current_contig`. Print the return from `&reverse_comp` and a new line character to the output file.

When you are done your script should run using the command:

```
scripts/rev_comp.pl /homes/sheltonj/solutions/mini.fasta
```

Upload your finished script to KSOL.

##Contents of /homes/sheltonj/solutions/mini.fasta

```
>seq_1
TNNnActg
>seq_2
aatNNnAc
CCCGgggt
act
```

##Correct contents of your output file

```
>seq_1
cagTnNNA
>seq_2
agtacccCGGGgTnNNattTNNnActg
```

####An extra problem

If you solved this problem and want more than you should try to wrap the sequence in your output fasta file for extra credit.
