## awk

awk '{print $1}'

awk -F '.' '{print $3}'


-F : 以 xx 为分隔符

打印第 1,2 列 cat  test | awk -F',' '{print $1,$2}

打印最后一列 | awk -F',' '{print $NF}

统计列数: awk  '{print NF}'

取最后一行:  awk 'END {print}'

