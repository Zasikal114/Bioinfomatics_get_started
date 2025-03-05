1. `wc test_command.gtf`
2. `grep '^chr_' test_command.gtf | grep 'YDL248W'`
3. `sed 's/chr_/chromosome_/g' test_command.gtf | awk '{print $1, $3, $4, $5}'`
4. `awk '{temp=$2; $2=$3; $3=temp; print}' test_command.gtf | sort -k4,4n -k5,5n > result.gtf`
5. ```
   ls -l test_command.gtf
   chmod 774 test_command.gtf
   ls -l test_command.gtf
   ```
