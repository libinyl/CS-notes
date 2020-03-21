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