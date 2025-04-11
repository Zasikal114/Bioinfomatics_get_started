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
