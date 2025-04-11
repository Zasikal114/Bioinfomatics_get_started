### (1)
单端分析测序结果
```
test@bioinfo_docker:~/bedtools$ samtools flagstat COAD.ACTB.bam
……
0 + 0 paired in sequencing
……
0 + 0 properly paired (N/A : N/A)
……
```
### (2)
Secondary Alignment,即次要比对，指的是在一条测序read比对到基因组多个位置的情况下，同一read在其他位置的比对结果（通常是次优）

有4623条
```
test@bioinfo_docker:~/bedtools$ samtools view -f 256 COAD.ACTB.bam | wc -l
4923
```
### (3)
```
awk '$3 == "exon" {print $1 "\t" $4-1 "\t" $5 "\t" $9}' hg38.ACTB.gff | sort -k1,1 -k2,2n > ACTB.exons.sorted.bed
bedtools merge -i ACTB.exons.sorted.bed > ACTB.exons.merged.bed
awk '$3 == "gene" {print $1 "\t" $4-1 "\t" $5 "\t" $9}' hg38.ACTB.gff | sort -k1,1 -k2,2n > ACTB.gene.sorted.bed
bedtools subtract -a ACTB.gene.sorted.bed -b ACTB.exons.merged.bed > ACTB.introns.bed
bedtools intersect -a COAD.ACTB.bam -b ACTB.introns.bed -ubam > COAD.ACTB.introns.bam
samtools fastq COAD.ACTB.introns.bam > COAD.ACTB.introns.fastq
```
### (4)
```
samtools sort COAD.ACTB.bam -o COAD.ACTB.sorted.bam
samtools index COAD.ACTB.sorted.bam
bedtools genomecov -ibam COAD.ACTB.sorted.bam -bga -split > COAD.ACTB.coverage.bedgraph
```
