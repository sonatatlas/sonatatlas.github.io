---
title: System Q&A
categories: back-pages
tags: system
layout: default
---
[3]: https://stackoverflow.com/questions/200469/what-is-the-difference-between-a-process-and-a-thread?page=1&tab=active#tab-top
[2]: https://softwareengineering.stackexchange.com/questions/325601/is-a-while-loop-intrinsically-a-recursion/325669
[1]: https://stackoverflow.com/questions/19452360/how-exactly-stdin-stdout-stderr-are-implemented-in-linux
[0]: https://stackoverflow.com/questions/42426816/how-does-waitnull-exactly-work?rq=1

[3-0]: https://stackoverflow.com/users/893/greg-hewgill
[2-0]: https://softwareengineering.stackexchange.com/users/7422/kilian-foth
[1-0]: https://stackoverflow.com/users/166749/fred-foo
[0-0]: https://stackoverflow.com/users/6530695/tony-tannous

# 03
## What is the difference between a process and a thread? - [StackOverflow][3]
> __Threads shared memory.__

> Linus - [proc fs and shared pids.](http://lkml.iu.edu/hypermail/linux/kernel/9608/0191.html)

Both processes and threads are independent sequences of execution. The typical difference is that threads (of the same process) run in a shared memory space, while processes run in separate memory spaces.

I'm not sure what "hardware" vs "software" threads you might be referring to. Threads are an operating environment feature, rather than a CPU feature (though the CPU typically has operations that make threads efficient).

Erlang uses the term "process" because it does not expose a shared-memory multiprogramming model. Calling them "threads" would imply that they have shared memory.

[@Greg Hewgill][3-0]

# 02 
## Is a while loop intrinsically a recursion? - [StackExchange][2]
> Recursion is more useful.

Loops are very much not recursion. In fact, they are the prime example of the opposite mechanism: iteration.

+ The point of __recursion__ is that one element of processing calls another instance of itself. 

+ The __loop__ control machinery merely jumps back to the point where it started.

Jumping around in code and calling another block of code are different operations. For instance, when you jump to the start of the loop, the loop control variable still has the same value it had before the jump. But if you call another instance of the routine you're in, then the new instance has new, unrelated copies of all of its variables. Effectively, one variable can have one value on the first level of processing and another value on a lower level.

This capability is crucial for many recursive algorithms to work, and this is why you can't emulate recursion via iteration without also managing a stack of called frames which keeps track of all those values.

[@Kilian Foth][2-0]

# 01
## How exactly stdin, stdout, stderr are implemented in linux? -- [Stackoverflow][1]

stdin, stderr, and stdout are file descriptors (or FILE* wrappers around them, if you mean the C stdio objects bearing those names). File descriptors are numbers that index a per-process data structure in the kernel. That data structure records which I/O channels a process has open, I/O channel being my ad-hoc term for a file, device, socket, or pipe.

By convention, the first entry in the table has index 0 and is called the standard input, 1 is the standard output and 2 is the standard error channel. This is just a convention in Unix programs; as far as the kernel is concerned, nothing's special about these numbers.

Each I/O system call (read, write, etc.) takes a file descriptor that indicates which channel the call should operate on.

[@Fred Foo][1-0]

# 00
## How does wait(NULL) exactly work? - [Stackoverflow][0]

wait(NULL) will block parent process until any of its children has finished. If child terminates before parent process reaches wait(NULL) then the child process turns to a zombie process until its parent waits on it and its released from memory.

If parent process doesn't wait for its child, and parent finishes first, then the child process becomes orphan and is assigned to init as its child. And init will wait and release the process entry in the process table.

In other words: parent process will be blocked until child process returns an exit status to the operating system which is then returned to parent process. If child finishes before parent reaches wait(NULL) then it will read the exit status, release the process entry in the process table and continue execution until it finishes as well.

[@Tony Tannous][0-0]
