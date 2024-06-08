# linux
Here, I will put some of the most important Linux commands and their possible explanations, these commands are used most of the time for any data, file manipulation or to monitor the processor, networking etc 

Common Linux Commands
Process:
find the open process : netstat -tulp
find the status of any specific process - ps aux | grep mysql
To kill any user session from linux
w
ps -ft tty
kill pid

System performance:
To see the Memory & CPU utilisation
Every process is given a specified amount of time to run on the CPU. The actual time for which the process is running on the CPU is called the virtual runtime of the process.

command : vmstat 

procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 0  0      0 287788 143396 2847152    0    0     9     4    1    1  0  0 100  0  0


	Procs
r: number of processes waiting for run time.
b: number of processes in uninterruptible sleep.
Memory
swpd: amount of virtual memory used.
free: amount of idle memory.
buff: the amount of memory used as buffers.
cache: amount of memory used as cache.
Swap
si: memory swapped in from disk (/s).
so: memory swapped to disk (/s).
IO
bi: Blocks received from a block device (blocks/s).
bo: Blocks sent to a block device (blocks/s).
System
in: number of interrupts per second, including the clock.
cs: number of context switches per second.
CPU – These are percentages of total CPU time.
us: Time spent running non-kernel code. (user time, including nice time)
sy: Time spent running kernel code. (system time)
id: Time spent idle. Before Linux 2.5.41, this includes IO-wait time.
wa: Time spent waiting for IO. Before Linux 2.5.41, included in idle.
st: Time stolen from a virtual machine. Before Linux 2.6.11, unknown.


Network Troubleshooting | Linux specific

Static routes:
	route -n  Old style or depricated
	ip route show or ip r [ New style ]

TCP: It is a Layer 4 protocol along with UDP

![img-1](https://github.com/partho-dev/linux/assets/150241170/c0d4e0ec-6cb3-4ce0-a2fe-55a644a97555)

