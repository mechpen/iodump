# iodump

Dump file descriptor traffic.

## Requirement

- bcc

## Example

In one terminal:
```
$ cat
hello world!
hello world!
second line!
second line!
```

Pid of `cat` is 11948.  Dump all io traffic:
```
# ./iodump.py 11948
waiting for data
11:45:51.067 WR >>> pid 11948 fd 1 len 13(13)
0000  68 65 6c 6c 6f 20 77 6f  72 6c 64 21 0a           hello world!.
11:46:13.923 RD <<< pid 11948 fd 0 len 13(13)
0000  73 65 63 6f 6e 64 20 6c  69 6e 65 21 0a           second line!.
11:46:13.924 WR >>> pid 11948 fd 1 len 13(13)
0000  73 65 63 6f 6e 64 20 6c  69 6e 65 21 0a           second line!.
11:46:25.987 RD <<< pid 11948 fd 0 len 0(0)
^C
4 packets captured
```

The first `RD` is missing because `ksys_read()` is already called
before `iodump`.

## Todo

1. sniff a program name

2. sniff other syscalls: readv/writev, sendmsg/recvmsg, and etc.
