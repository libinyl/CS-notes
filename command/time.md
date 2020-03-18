## time

默认格式:

```
%Uuser %Ssystem %Eelapsed %PCPU (%Xtext+%Ddata %Mmax)k
%Iinputs+%Ooutputs (%Fmajor+%Rminor)pagefaults %Wswaps
```

例子

```shell
#!/bin/sh
#user time, system time, real time, and maximum memory usage
/usr/bin/time -f '%Uu %Ss %er %MkB %C' "$@" 
```


## c time

time_t  time1 = time(NULL);//获取系统时间，单位为秒, 从 1970 至今