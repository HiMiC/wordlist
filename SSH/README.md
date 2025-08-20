
Генерация словарей

https://hackware.ru/?p=15350#8
https://www.securitylab.ru/analytics/541481.php


```
hashcat -a 1 --stdout ssh-priv-key.txt files_ext.txt > ssh_ext.txt

hashcat -a 1 --stdout dir.txt ssh_ext.txt > ssh_dir_ext.txt

hashcat -a 1 --stdout dir.txt files_backup.txt > ssh_dir_backup.txt

cat  ssh-priv-key.txt ssh_ext.txt ssh_dir_ext.txt files_backup.txt  ssh_dir_backup.txt > all.txt

```