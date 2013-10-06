##signal handler
内核给一个进程发送软中断信号的方法，是在进程所在的进程表项的信号域设置对应于该信号的位。


## singal - ANSI C signal handling

## signal 
regular signal [1, 31]
real time signal [32, 64]

real time signal 与 reagular signal 的区别在于每一次发送的real time signal 都会被加入悬挂信号队列， 所以多次发送的 real time signal 会被缓存起来。而同一种regular signal 不会被缓存， 即如果同一个signal 被发送多次， 它们只会有一个会被放入接受进程的悬挂队列。

##synopsis

```
#include <signal.h>
typedef void (/*sighandler_t) (int);
sighandler_t signal (int signum, sighandler_t handler);
```


##description

	The behavior of `signal()` varies across UNIX versions, and has also varied histroically across different  versions of Linux. Avoid its use: use `sigaction(2)` instead. See Portability below.

	`signal()` sets the disposition of the signal signum to handler, which is either SIG_IGN, SIG_DFL, or the addresso of a programmer-defined function(a "signal handler")

	If the signal signum is delivered to the process, then one of the following happens:

	- If the disposition is set to SIG_IGN, then the signal is ignored.
	- If the disposition is set to SIG_DFL, then the default action associated with the signal occurs.
	- If the disposition is set to a function, the first either the disposition is reset to SIG_DFL, or the signal is blocked (see portability below), and then handler is called with argument signum. If invocation of the handler caused the signal to be blocked, then the signal is unblocked upon return from the handler.

	The signals SIGKILL and SIGSTOP cannot be caught or ignored.

##Signal dispositions

	Each signal has a current disposition, which determines how the process behaves when it is delivered the signal.

	The entries in the "Action" column of the tables below specify the defult disposition for each signal, as follows:

	* Term - Default action is to terminate the process.
	* Ign - Default action is to ignore the signal.
	* Core - Default action is to terminate the process and dump core (see core(5))
	* Stop - Default action is to stop the process.
	* Cont Default action is to continue the process if it is currently stopped.

	A process can change the disposition of a signal using sigaction or signal. Using these system calls, a process can elect one of the following behaviors to occur on delivery of the signal: perform the default action; ignore the signal; or catch the signal with a signal handler, a programmer-defined function that is automatically invoked when the signal is delivered. (By default, the signal handler is invoked on the normal process stack. It is possible to arrange that the signal handler uses a alternate statck.)

	The signal disposition is per-process attribute: in a multithreaded application, the disposition of a particular signal is the same for all threads.

	A child created via fork inherits a copy of its parent's signal dispositions. During an execve, the dispositions of handled signals are reste tothe default; the dispositions of ignored signals are left unchanged.
