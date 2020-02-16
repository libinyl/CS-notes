## process

![](/images/process.png)

- R  running or runnable (on run queue)
- D  uninterruptible sleep (usually IO)
- S  interruptible sleep (waiting for an event to complete)
- Z  defunct/zombie, terminated but not reaped by its parent
- T  stopped, either by a job control signal or because it is being traced

https://idea.popcount.org/2012-12-11-linux-process-states/