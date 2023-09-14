`/Users/ymanasa/Library/CloudStorage/OneDrive-MichiganMedicine/bioinf_575/session2/variant_example.tsv.gz` has read information in each sample (column) for each gene (row)

cut -f1 will give first column of a tsv 
>>>  gzip -dc variant_example.tsv.gz | cut -f1
ENSG00000284526.1
ENSG00000284534.1
ENSG00000284540.1
ENSG00000284543.1
ENSG00000284553.1
ENSG00000284554.1

'-f' : field 

>>> gzip -dc variant_example.tsv.gz | cut -f1,5 
gives columns 1 and 5. for columns 1 through 5 (cut -f1-5)

>>> head
gives first 3 lines 

>>> gzip -dc variant_example.tsv.gz | head -n1 | grep -o '\t' | wc -l 
returns number of tabs in the first line of the file. since this is a tsv file, the number of tabs in one line tells us how many columns are in the file 


>>> gzip -dc case2_variant.vcf.gz| grep -v '^#' | wc -l
the '^' is to pick lines that start with '#'' or whatever character follows '^' 
grep -v 'foo' argument: grep everything except 'foo' 


>>> cut -d " " -f1 test_count.txt | uniq -c
counts unique elements in first column BUT uniq counts elements with same values but on non consecutive lines as different elements so we need to sort first
 1 B
 1 C
 2 B
 3 A

>>> cut -d " " -f1 test_count.txt | sort | uniq -c
sorted alphabetically and then counting uniq elements 
 3 A
 3 B
 1 C

>>> gzip -dc case2_variant.vcf.gz| grep -v '^#'| cut -f1| sort| uniq -c
will give us the count for all the different chromosomes in the file
there is only one chromosome in the file: Y 
but there are 959 lines of data for Y 

>>>  gzip -dc case2_variant.vcf.gz| grep -v '^##' | head
to see the first 10 lines that do not start with ## 

/# CHROM POS ID REF ALT QUAL FILTER INFO
Y 2728456 rs2058276 T C 32 . AC=2;AN=2;DB;DP=182;H2;NS=65
Y 2734240 . G A 31 . AC=1;AN=2;DP=196;NS=63
Y 2743242 . C T 25 . AC=1;AN=2;DP=275;NS=66
Y 2746727 . A G 34 . AC=2;AN=2;DP=179;NS=64
Y 2777970 . T A 67 . AC=1;AN=2;DP=225;NS=67
Y 2782506 rs2075640 A G 38 . AC=1;AN=2;DB;DP=254;H2;NS=66
Y 2783755 . G A 51 . AC=1;AN=2;DP=217;NS=67
Y 2788927 rs56004558 A G 38 . AC=1;AN=2;DB;DP=173;NS=60
Y 2813908 . T G 46 . AC=1;AN=2;DP=188;NS=67

>>> gzip -dc case2_variant.vcf.gz| grep -v '^#'| cut -f4,5 | sort | uniq -c
to sort and count unique elements in the 4th and 5th column 
  34 A C
 155 A G
  26 A T
  56 C A
  49 C G
 175 C T
 163 G A
  46 G C
  53 G T
  35 T A
 124 T C
  43 T G

>>> history | cut -c 8- | tail -n 50 > commands_bash_090723.txt
save the last 50 terminal commands to a txt file

>>> grep -v '>' BRCA1_sequence.fa | head -n 2 > DNA_seq.txt
to get the first 2 lines, excluding the first descriptor line that has '>'

>>> tr ATGC TACG < DNA_seq.txt | tr "\n" _ | rev
replaces all the As with Ts, Ts with As, G with Cs, C with Gs in DNA_seq.txt | replace new lines with _ so that rev can reverse the entire RNA sequence to correctly translate 


>>> grep -o ATGC BRCA1_seq.fasta
will search for ATGC pattern. it will not tell you where they are unless we dont use the -o flag
WARNING: if there is a sequence: ATGATGA and we grep ATGA, it will only show the first ATGA and ignore the next one because of the overlap  

>>> sed "s/ATAGGAT/X\n/g" BRCA1_sequence.fa | grep X | wc -l
will replace ATAGGAT with X and new line then we find all the X's and then count the number of these occurrences using wc -l 

>>> grep -o [GC] BRCA1_sequence.fa | wc -l
square brackets can be used to match multiple letters 

>>> grep -v '^#' TNBC_sample.vcf | awk '$1\==1 && $6\==24' 
this will exclude lines starting with # and then search for lines in column 1 that have value of 1 and will search through column 6 to find rows that have a value of 24. we can use wc -l to count the occurrences 