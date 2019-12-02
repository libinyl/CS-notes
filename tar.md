tar -xvf file.tar //?? tar?

tar -xzvf file.tar.gz //??tar.gz

tar -xjvf file.tar.bz2   //?? tar.bz2

tar -xZvf file.tar.Z   //??tar.Z

unrar e file.rar //??rar

unzip file.zip //??zip


xz -d  // ?? xz

## 各种后缀的区别及打开方式

https://www.thomas-krenn.com/en/wiki/Archive_under_Linux_(tar,_gz,_bz2,_zip)

tar: Tape Archiver

## 常用选项

选项 | 作用
---|---
-x | extract 解压
-z | gzip 相关
-j | bzip2 相关
-v | verbose
-f | file=archive,通常都要指定

## 特定类型常用选项

tar | tar -xvf
----|---------
tar.gz | tar -xzvf
tar.bz2 | tar -xjvf
tar.Z | tar -xZvf
xz | xz -d

