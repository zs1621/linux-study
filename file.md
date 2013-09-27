
## file descriptor

**file descriptor(FD)** is an abstract indicator for accessing a file. The term is generally used in `POSIX operatinng systems`

in POSIX, a file descriptor is an integer, specifically of the C type init. there are three standard POSIX file descriptors.corredsponding to the three standard streams, which presumbaly every process(save perhaps a daemon) should expect to have:

> 0: Standard input(stdin)
  1: Standard output(stdout)
  2: Standard error(stderr)

 Generally, a file descriptor is an index for an entry in a kenel-resident array data structure containing the details of open files. in POSIX this data structure is called a file descriptor table, and each process has its own file descriptor table. The process passes the file descriptor to the kernel through a system call, and the kernel will access the file on behalf of the process. The process itself cannot read or write hte file descriptor table directly.


 on Linux, the set of file descriptors open in a process can be accessed under the /proc/PID/fd/, where PID is the process indentifier.

 in Unix-like systems, file descriptors can refer to any Unix file type named in a file system. As well as regular files, this includes directories, block and charactor devices(also called 'special files'), Unix domain sockets, and named pipes .  File descriptors can also refer to other objects that do not normally exist in the file system, such as anonymous pipes and network sockets.
