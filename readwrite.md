## read

read:

       ssize_t read(int fd, void *buf, size_t count);

从 fd, 尝试读取 count 个字节到 buf 中.

如果读到了 eof, 读取完, 且返回 0;

如果还没读到 eof,但读取了 count 个字节,则返回实际读取的字节.

## write

write:

       ssize_t write(int fd, const void *buf, size_t count);

向fd 写入buf 中最多count个字节的数据.

1) 写入成功, 则返回实际写入的字节数
2) 写入出错,返回 -1



