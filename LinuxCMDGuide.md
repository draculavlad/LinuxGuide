Hot Key Guide

```
alt+f                       skip to next word
alt+b                       skip to last word
ctrl+a                      jump to start of the commad
history                     print all recorded bash command 



grep -e $pattern1 -e $pattern2 files          search content in files
find path -name $pattern                      search file by name
ps -ef |grep $pid                             search process by pid
netstat -tunlp |grep $port                    search process by port no
cat <<EOF > filename ... EOF                  write file with EOF
                            
strace -o $filepath -f -e recvfrom,sendto -Ttt -p $pid -s $length           dump initial $length of tcp content to $filepath in process whose id is $pid  

ss -s             summary for all connection
netstat -nap |wc -l       total count for all connection
netstat -nap |grep $pid|wc -l       total count for all connection of process whose id us $pid
```
