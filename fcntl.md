##Synopsis

```
#include <unistd.h>
#include <fnctl.h>
int fcntl(int fd, int cmd, ... /*arg*/);

```

##Description
`fcntl()` performs one of the operations described below on the open file descriptor `fd`. The operation is determined by `cmd`.

`fcntl()` can take an optional third argument. Whether or not this argument is required is determined by cmd. The required argument type is indicated in parenthese after each `cmd name`(in most cases, the required type is `int`, and we indentify the argument the name `arg`), or `void` is specified if the argument is not requried.


### Duplicating a file descriptor

*F_DUPFD*(int)
	
	Find the lowest numbered available file descriptor greater than or equal to arg and make it be a copy of fd. This is different from `dup2`, which uses exactly the descriptor specified.
	on success, the new descriptor is returned.

*F_DUPFD_CLOEXEC*

	As for F_DUPFD, but additionally set the close-on-exec flag for the duplicate descriptor. Specifying this flag permits a program to avoid an additional `fcntl() F_SETFD` operation to set the FD_CLOEXEC flag. For an explanation of why this 


### File descriptor flags

The following commands manipulate the flags associated with a file descriptor. Currently, only one such flag is defined: FD_CLOEXEC, the close-on-exec flag. if the FD_CLOEXEC bit is 0, the file descriptor will remain open accross an execve(), otherwise it will be closed.

F_GETFD(void)

	Read the file descriptor; arg is ignored.

F_SETFD(int)

	Set the file descriptor flags to the value specified by arg.


### File status flags

Each open file description has certain associated status flags, initialized by open() and possibly modified by fcntl(). Duplicated file descriptors refer to the same open file description, and thus share the same file status flags.

The file status flags and their semantics are described in open


F_GETFL (void)
	
	Get the file access mode and the file status flags; arg is ignored.

F_SETFL (int)
	
	Set the file status flags to the value specified by arg. File access mode (O_RDONLY, O_WRONLY, O_RDWR) and file creation flags (ie., O_CREAT, O_EXCL, O_NOCTTY, O_TRUNC) in arg are ignored. On Linux this command can change only the O_APPEND, O_ASYNC, O_DIRECT, O_NOATIME and O_NONBLOCK flags.
