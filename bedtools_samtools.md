## bedtools/samtools部分
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
## homework部分
### 人类基因组
人类基因组大小：3.1Gb（NCBI;GRCh38.p14;Feb 3, 2022）
- 人类基因组基本组成：
  - 编码区
    - 蛋白质编码基因
    - 调控序列
  - 非编码区
    - 重复序列
    - 非编码RNA基因
    - 假基因
    - 保守非编码区
### 人类非编码RNA
总计41970个，数据来自https://www.gencodegenes.org/human/stats.html
| RNA类型 | 基因数目 | 功能 |
|:----:|:-----:|:----:|
|lncRNA|34914|调控基因表达，参与染色质修饰、转录调控、RNA剪切、表观遗传调控等|
|miRNA|1879|通过结合靶标mRNA的3'非翻译区（UTR），抑制翻译或降解mRNA，调控基因表达|
|misc_RNA|2208|-|
|Mt_rRNA|2|参与线粒体核糖体组装，介导线粒体内蛋白质的翻译|
|Mt_tRNA|22|在线粒体翻译过程中转运特定氨基酸，参与线粒体蛋白合成|
|rRNA|47|构成核糖体的核心结构，直接参与mRNA翻译成蛋白质的催化过程|
|scaRNA|49|定位于细胞核的卡哈尔体（Cajal body），指导snRNA的化学修饰|
|scRNA|1|-|
|snoRNA|942|在核仁中指导rRNA的化学修饰|
|snRNA|1901|参与剪接体组装，调控pre-mRNA的剪切和拼接|
|sRNA|5|-|




