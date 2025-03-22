（1）

BWT对原始序列进行高效压缩，同时通过生成索引在压缩数据上直接进行高效的字符串匹配，并且通过 backward search 算法在线性时间内快速定位匹配的子串。从而提高了运算速度。

BWT对原始序列进行高效压缩，同时对数据分块处理，并辅助以FW-index等数据结构。

（2）
```
test@bioinfo_docker:~/mapping$ bowtie -v 2 -m 10 --best --strata BowtieIndex/YeastGenome -f THA2.fa -S THA2.sam
# reads processed: 1250
# reads with at least one reported alignment: 1158 (92.64%)
# reads that failed to align: 77 (6.16%)
# reads with alignments suppressed due to -m: 15 (1.20%)
Reported 1158 alignments to 1 output stream(s)
test@bioinfo_docker:~/mapping$ grep -v '^@' THA2.sam | cut -f 3 | sort | uniq -c
     92 *
     18 chrI
     51 chrII
     15 chrIII
    194 chrIV
     25 chrIX
     12 chrmt
     33 chrV
     17 chrVI
    125 chrVII
     68 chrVIII
     71 chrX
     56 chrXI
    169 chrXII
     67 chrXIII
     58 chrXIV
    101 chrXV
     78 chrXVI
```
（3.1）CIGAR string 是 SAM/BAM 文件中的一个字段，由一系列数字和操作符组成，包含reads比对到参考基因组的比对方式信息。
其中 CIGAR 是 "Compact Idiosyncratic Gapped Alignment Report" 的缩写。
操作符包括：
- M：匹配或错配（read 的碱基与参考基因组匹配或错配）。
- I：插入（read 中有而参考基因组中没有的碱基）。
- D：删除（参考基因组中有而 read 中没有的碱基）。
- N：跳过（参考基因组中的一段区域，如内含子）。
- S：软剪切（read 的一部分未比对到参考基因组，但这些碱基仍保留在 read 中）。
- H：硬剪切（read 的一部分未比对到参考基因组，且这些碱基不包含在 read 中）。
- =：完全匹配。
- X：错配。
（3.2）Soft clip 表示 read 的一部分未比对到参考基因组，但这些碱基仍然保留在 read 中， 用 S 表示。
（3.3）Mapping quality (MAPQ) 是 SAM/BAM 文件中的一个字段，表示 reads 比对到参考基因组的可靠性。
它是一个 Phred 质量分数，计算公式为：MAPQ = -10 * log10(P)，其中 P 是比对错误的概率。
取值范围一般为从0到60。
MAPQ 越高，read 比对到参考基因组的置信度越高。
MAPQ 低可能表示 read 比对到多个位置（多重比对）或比对质量差。
