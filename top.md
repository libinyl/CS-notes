## top

https://www.cnblogs.com/peida/archive/2012/12/24/2831353.html

us: 用户空间占用CPU百分比

%us — 用户空间占用CPU的百分比。

%sy — 内核空间占用CPU的百分比。

%ni — 改变过优先级的进程占用CPU的百分比

%id — 空闲CPU百分比

%wa — IO等待占用CPU的百分比

%hi — 硬中断（Hardware IRQ）占用CPU的百分比

%si — 软中断（Software Interrupts）占用CPU的百分比

PID — 进程id

USER — 进程所有者

PR — 进程优先级

NI — nice值。负值表示高优先级，正值表示低优先级

VIRT — 进程使用的虚拟内存总量，单位kb。VIRT=SWAP+RES

RES — 进程使用的、未被换出的物理内存大小，单位kb。RES=CODE+DATA

SHR — 共享内存大小，单位kb

S — 进程状态。D=不可中断的睡眠状态 R=运行 S=睡眠 T=跟踪/停止 Z=僵尸进程

%CPU — 上次更新到现在的CPU时间占用百分比

%MEM — 进程使用的物理内存百分比

TIME+ — 进程使用的CPU时间总计，单位1/100秒

COMMAND — 进程名称（命令名/命令行） 