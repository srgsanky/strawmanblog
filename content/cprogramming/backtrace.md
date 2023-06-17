---
title: "Backtrace"
date: 2023-06-16T18:39:50-07:00
draft: false 
---

## Introduction

When a program halts abruptly, it is very useful to find out the stack trace of the
thread that caused the program to halt. Unfortunately, printing the stacktrace/backtrace
in C is not an out of the box functionality provided by the language. We need libraries
or use existing tools like debuggers to print the backtrace.

## Using GDB (linux) or LLDB (mac)

### LLDB

Save the following in .lldbinit

```
target stop-hook add --one-liner "thread backtrace"
```

Now run the program under lldb

```bash
lldb --no-lldbinit --source-quietly \
    --source .lldbinit \
    cmake-build-debug/TryPointers \
    --one-line "process launch"
```

{{< highlight bash "linenos=inline,hl_lines=4,linenostart=1" >}}
lldb --no-lldbinit --source-quietly \
    --source .lldbinit \
    cmake-build-debug/TryPointers \
    --one-line "process launch"
{{< / highlight >}}

This will print a backtrace with symbols, filename and line number whenever the program is
stopped due to a signal. Here is an example

```
* thread #1, queue = 'com.apple.main-thread', stop reason = EXC_BAD_ACCESS (code=1, address=0x0)
  * frame #0: 0x000000010000399c TryPointers`b_print_matrix(matrix_ptr=0x0000000000000000, num_rows=10, num_columns=5) at matrix_bulk_allocated.c:22:28
    frame #1: 0x0000000100003590 TryPointers`main at main.c:66:5
    frame #2: 0x000000010001108c dyld`start + 520
```
