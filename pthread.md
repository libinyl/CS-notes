## pthread

pthread_join: A 线程调用pthread_join(B) 用来等待 B 结束并获取其返回值. 于是A 和 B join(汇合)在了一起.

pthread_detach: 可以在 A 线程中 pthread_detach(A), 也可以在 B 线程中 pthread_detach(A), 表示不再需要等待 A 的结束,不需要 A 的返回值. 通常用于创建新线程后立即调用,表明此意,节省资源. https://stackoverflow.com/a/22427298