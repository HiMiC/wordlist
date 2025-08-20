
# Словари для поиска SSH ключей в WEB

Генерация словарей

https://hackware.ru/?p=15350#8

https://www.securitylab.ru/analytics/541481.php


```
hashcat -a 1 --stdout ssh-priv-key.txt files_ext.txt > w_ext.txt

hashcat -a 1 --stdout files_dir.txt w_ext.txt > w_dir_ext.txt

hashcat -a 1 --stdout files_dir.txt files_backup.txt > w_dir_backup.txt

cat  ssh-priv-key.txt w_ext.txt w_dir_ext.txt files_backup.txt  w_dir_backup.txt > all.txt
```