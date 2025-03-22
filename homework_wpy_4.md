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
