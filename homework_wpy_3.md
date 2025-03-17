```
#!/bin/bash
folder_path="bash_homework"
if [ ! -d "$folder_path" ]; then
  echo "$folder_path  don't exsit"
  exit 1
fi
> filenames.txt
> dirnames.txt
for item in "$folder_path"/*; do
  if [ -f "$item" ]; then
       echo "$(basename "$item")" >> filenames.txt
  elif [ -d "$item" ]; then
   
    echo "$(basename "$item")" >> dirnames.txt
  fi
done
echo "it's done"
```
```
a1.txt
a.txt
b1.txt
bam_wig.sh
b.filter_random.pl
c1.txt
chrom.size
c.txt
d1.txt
dir.txt
e1.txt
f1.txt
human_geneExp.txt
if.sh
image
insitiue.txt
mouse_geneExp.txt
name.txt
number.sh
out.bw
random.sh
read.sh
test3.sh
test4.sh
test.sh
test.txt
wigToBigWig
```
```
a-docker
app
backup
bin
biosoft
c1-RBPanno
datatable
db
download
e-annotation
exRNA
genome
git
highcharts
home
hub29
ibme
l-lwl
map2
mljs
module
mogproject
node_modules
perl5
postar2
postar_app
postar.docker
RBP_map
rout
script
script_backup
software
tcga
test
tmp
tmp_script
var
x-rbp
```
