## sed

:qstream editor

sed -i (in-place, 原地修改)


sed -i 's/原字符串/新字符串/' /home/1.txt
sed -i 's/原字符串/新字符串/g' /home/1.txt

中间的 's/aa/bb' 即将原来的 aa 替换为 bb, 加上 g 之后就是 global

清理: 



-n选项：只显示匹配处理的行（否则会输出所有）（也就是关闭默认的输出）

## 正则

