
2023-05-08

HAL(hardware abstraction layer)

![[kernel.png]]

passport office example was good for the use of kernel 

User space vs Kernel space

in user space it is mostly restricted environment
Kernel can have more control over hardware

toolchain is used to convert the code for intel based processor to arm based processor

argo project 

https://argoproj.github.io/

arm based architecture
![[IMG_5354.heic]]




 loadable kernel module (LKM) is **an object file that contains code to extend the running kernel, or so-called base kernel, of an operating system**. LKMs are typically used to add support for new hardware (as device drivers) and/or filesystems, or for adding system calls.


when a hot pluggable new devide is inserted the devide driver which is an LKM gets loaded automatically to the kernel


  

A cross-compiler is a compiler where the target is different from the host. A toolchain is **the set of compiler + linker + librarian + any other tools you need to produce the executable (+ shared libraries, etc) for the target**. A debugger and/or IDE may also count as part of a toolchain



insmod for loading 
and 
for removing 

rmmode

![[Pasted image 20230508114530.png]]
![[Pasted image 20230508114537.png]]



watchdog reset the kernel

A watchdog timer is **a device or software that performs a specific operation after a certain period of time if the system or program stops its regular service and then it does not recover on its own**.


TI-A15 MPU board 

printk is a C function from the Linux kernel interface that prints messages to the kernel log. It accepts a string parameter called the format string, which specifies a method for rendering an arbitrary number of varied data type parameter into a string. The string is then printed to the kernel log.

![[Pasted image 20230508121403.png]]

question:

how debugger or debugging works in kernel programming ?
>printk or kernel logs are there 
>gdb for debigging and there is kgdb there is for debugging 

how root user works in linux ?

>mast se aap kernel ko kill kar sakte ho kernel ko delete bhi kar sakte ho 