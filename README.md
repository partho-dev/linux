# linux
Here, I will put some of the most important Linux commands and their possible explanations, these commands are used most of the time for any data, file manipulation or to monitor the processor, networking etc 

# **Common Linux Commands**
### Process:
- find the open process : netstat -tulp
- find the status of any specific process - ps aux | grep mysql
- To kill any user session from linux
				w
				ps -ft tty
				kill pid

### System performance:
To see the Memory & CPU utilisation
Every process is given a specified amount of time to run on the CPU. 
The actual time for which the process is running on the CPU is called the `virtual runtime` of the process.

command : `vmstat` 

``` 
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 0  0      0 287788 143396 2847152    0    0     9     4    1    1  0  0 100  0  0

```




- Procs
		r: number of processes waiting for run time.
		b: number of processes in uninterruptible sleep.
- Memory
		swpd: amount of virtual memory used.
		free: amount of idle memory.
		buff: the amount of memory used as buffers.
		cache: amount of memory used as cache.
- Swap
		si: memory swapped in from disk (/s).
		so: memory swapped to disk (/s).
		IO
		bi: Blocks received from a block device (blocks/s).
		bo: Blocks sent to a block device (blocks/s).
- System
		in: number of interrupts per second, including the clock.
		cs: number of context switches per second.
- CPU – These are percentages of total CPU time.
		us: Time spent running non-kernel code. (user time, including nice time)
		sy: Time spent running kernel code. (system time)
		id: Time spent idle. Before Linux 2.5.41, this includes IO-wait time.
		wa: Time spent waiting for IO. Before Linux 2.5.41, included in idle.
		st: Time stolen from a virtual machine. Before Linux 2.6.11, unknown.


# Network Troubleshooting | Linux specific

## Static routes:
`route -n` ***Old style or depricated***
`ip route show` or 
`ip r` [ New style ]

### TCP: It is a Layer 4 protocol along with UDP

![img-1](https://github.com/partho-dev/linux/assets/150241170/c0d4e0ec-6cb3-4ce0-a2fe-55a644a97555)

1. It is a reliable protocol
2. It ensures the packet reaches to the target destination, 
3. if it does not get any acknowledgement, the packets are re-sent again
4. The data on Layer 4 are called as “Segment”
5. Segment --> Packet ---> Frame

## Linux File system : 
	The file system hierarchy of linux is very important to understand.
	based on the usage of the server [Web server, file server ] the partitions can be mounted.

For example, if its a `file server`, the most important partition would be `/home` 
so, it is recommended to have a separate partition on the server.
	/tmp is always recommended to have separate partitions.
	/var/www would be required to have a separate partition for the web server.

`/home` is used to store all the user information (user profiles), if a new user “partho” is created, there will be a new directory created automatically under `/home` as `/home/partho`

- /usr - this is used to store all information about any application that is installed on the server, [ Apps are stored here ]
- /etc  ***et-see*** this is used to store all configuration related information about the server, it is always recommended to keep a backup of this [ cp /etc /etc.old]
- /boot - Most important, this contains all the information about the kernel
- /bin - Binary - normal executables file or commands are stored here [ cp, mv etc ] - any user can be allowed to execute this commands, this commands are not destructive to the machines.
- /sbin - sysadmin binary - This commands or executables are available only to root user or sudo users. [ permission denied]

![Lin-FS](https://github.com/partho-dev/linux/assets/150241170/abdb4c77-58cb-4674-8069-06875665c869)
based on the application, the partitions needs to be mounted separate, for an example.

![Lin-FS-2](https://github.com/partho-dev/linux/assets/150241170/e438d9c0-590c-4296-a041-ffa08143c0f9)

It is always recommended to have separate partitions on disk and each partitions should be mounted on certain path.
		Most important.
		/home
		/tmp
		/var/log
		/boot 
Should be on a different mount point.


## Understanding the memories:

![Linux-Memory](https://github.com/partho-dev/linux/assets/150241170/58b99625-c694-44c2-a378-796ad2b15de2)

When we open a file from `Harddisk` it goes into `RAM` and all the changes in the file take place on the RAM itself. 
Hare, the OS takes the file from `HDD` and places it on the `RAM` and then
`CPU` talks with `RAM` to do the further changes on the file.

**Dirty file**: When the changes on the file is not saved [***File on RAM is NoT Equal to file on HDD***]
- Here, the file 2 on the disk has 10 lines of code, but when we wanted to edit that, we clicked on the file stored on harddisk, 
- when the file was opened, it goes and creates a small area for itself into RAM and then it gets edited.
- in this state, the file is called `Dirty File`.

but, once the changes are saved, its no longer a dirty file, but it remains `inactive file` until we do some activity on that file [ generally mouse or Keyboard strokes ]

- when the files are inactive on Memory [ waiting for instruction from CPU, like write, read, delete, close etc] , it `releases` its space from RAM and come to `SWAP memory` on the hard disk [ this is called `SWAP IN`]
- The moment, the CPU gives instruction to do some action on the file[write/read etc] the file immediately becomes `Active File` and goes into the RAM [`SWAP OUT`]

Note: 
file 2 is in Dirty state now
file 1 is in “inactive state now” - It will move to SWAP memory in sometime.

### Did you know?
1. Wrong concept : When RAM is full, the files move to SWAP memory.
2. Correct concept : When a file is inactive on RAM, it moves to SWAP memory, even though the RAM has enough free space.


## Which is much faster Memory in a system:
```
CPU L1 > CPU L2 > CPU L3 > RAM > HDD
```

**CPU has 3 cache memories**
1. M1 - Which has very less storage but, this is the most fastest in any computer
2. M2 - Which has little more storage than M1, But it is slower than M1
3. M3 - Which has little more storage than M2, But it is slower than M2

## What is Virtual Memory : 
- this is the combination of all the Memories in the system
- L1 + L2 + L3 + RAM + SWAP 

## Finding more commands
- Linux is all about to know how to look for the help, 
- It is not about how much command we learn or memorize.
- So, always use the “man” page of any command to know more about that.

`man command_name`

man = Manual
- But, the man page is useful only to know which command is needed to read the options for. For that it is important to know the commands. This is the limitation in this process.

- If you want to perform some task, but not sure about the command, then you can type the `keyword` on shell too get the information about the command.

**Example: You wanted to know how to create logical volume or how to add group.**
So, you can use this command

`man -k “logical volume”`
*** k - keyword ***
**Note:** 
this command can only be performed as a `root` user
If there is no output or
The output is “nothing appropriate”
- that means the index is not created on the system yet, probably the server was just configured/created.
- the system needs 24 hours to generate the indexes.
- but, there is a way to force the system to generate the DB index forcefully
- Execute the command “ mandb “  
- once the db indexing is completed the keyword will give related output
`man -k “keyword” `

once the keyword command gets the relevant command, it displays that with certain number into that
Note: 
In the man page, with the option, if there is anything `Capital` & `underlined`, that means that value needs to be supplied.

![man-1](https://github.com/partho-dev/linux/assets/150241170/776b37bc-4188-4c84-8b58-03b223737c4e)

-e --expiredate EXPIRE_DATE

![man-2](https://github.com/partho-dev/linux/assets/150241170/1953536a-cebd-49ab-903b-fad232fef3cc)

### Some useful commands:
Once login to the Linux server, to verify which user account you logged in 
`who am i` [This is very useful when work on multiple applications on the same server and each application is configured to work with different user permission.]
Example: The owner of Service-A is User1 -- > So, this will help you to execute any copy, move command as an owner.

To see the present working directory:
`pwd`  -- > This will help to identify the current absolute path of your working directory




# Managing files on the Linux.
CRUD activity on files
- Create a file (C)
	1. touch filename
- Read a File (R) 
	1. cat > file_name --- Write all the content and to save and exit, press CTRL+D
	cat >> file_name -- To append the file with new contents to save and exit, press CTRL+D
	But, using cat, the existing contents cannot be edited, 
- edit the content (U)
	vi file_name
		- press (i) to be on insert mode-- edit the existing contents on that file
		- press (esc) to exit from editing mode
		- Type :
		- press w - to write the changes
		- press q - to quite 
		- To delete some lines - number of lines dd 
			ex: 10 dd will delete 10 lines starting from the cursor pointer
		- To set the line numbers
			:set number or
			:set nu
		- To jump directly to a particular line number
			:line_number Example :10 This will take the cursor to 10th line
- Delete the file (D)
	rm -rf filename.txt
- To see the list of items on linux.
		ls -l 

![List-files](https://github.com/partho-dev/linux/assets/150241170/67703e10-3ce3-4386-8f11-917af473cafd)

Permission : Root User Other
Read : r : 4
Write : w : 2
Execute : x : 1


Link : 1 --> This means this file is a single file and it does not have any soft link or hard link.

- Soft link 
	ln -s /etc/nginx/sites-available/api.conf /etc/nginx/sites-enanled/api.conf
Hard link 

### alias : This helps to create some custom commands 
Format : `alias cls=clear`
	means : cls will execute clear at the backend

- To remove the alias, execute 
	unalias cls 

- But this alias is temporary, logoff and login back will remove all the alias.
To make it permanent : 


### How to run multiple commands at the same time
We can use ``;`` or `&&` in between two commands to get them executed one after the other

```
Example : 
mkdir folder_name
then cd to that folder

<!-- To execute them in same command -->
mkdir partho ; cd partho
or
mkdir partho && cd partho

<!-- For 1 the command will execute if there is any error in some middle, it will go to next command
For 2 if there is any error, it will not go to the next command, the cycle breaks -->
```
