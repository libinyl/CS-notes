## epoll

参考: IO 多路复用是什么意思？ - 罗志宇的回答 - 知乎
https://www.zhihu.com/question/32163005/answer/55772739

原补丁: http://www.xmailserver.org/linux-patches/nio-improve.html

man page: http://www.xmailserver.org/linux-patches/epoll_create.txt

socket 源码: https://www.cnblogs.com/sddai/p/5790414.html



**IO多路复用**

单个线程通过记录跟踪每一个Sock(I/O流)的状态.

其中包含了 复用/解复用 的概念.

![](https://pic2.zhimg.com/80/18d8525aceddb840ea4c131002716221_hd.jpg)

![](https://img-blog.csdn.net/20150211004044328?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3RwZWFjZQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

https://blog.csdn.net/qq_31833457/article/details/78495354

很多链接进来，epoll 会把他们都监视起来，然后像拨开关一样，谁有数据就拨向谁，然后调用相应的代码处理。



https://suchprogramming.com/epoll-in-3-easy-steps/

水平触发: 若一次读取数据没有读完,下次仍可读: 
边缘触发: 若一次读取数据没有读完,下次不可读: 只在状态改变时传递数据

select 和 poll 只支持水平触发.