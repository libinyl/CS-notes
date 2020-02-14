## awk

awk '{print $1}'

awk -F '.' '{print $3}'


-F : 以 xx 为分隔符

{print NF}  打印列数

统计列数: awk  '{print NF}'