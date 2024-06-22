There are already some system calls in xv6 operating system.Here, we see how can we add our own system call in xv6.

For adding system call in xv6,

```c
we need to modify following files :  
   1) syscall.c  
   2) syscall.h  
   3) sysproc.c  
   4) usys.S  
   5) user.h
```

**We will add system call to print our name;**

## 1.syscall.c file

This file contain array of function pointers for all system call functions.  
Add the below entry in this array .

```c
[SYS_get_name] sys_get_name
```

![[Pasted image 20240619200339.png]]

One more change is to be done in this file.  
We are not going to write implementation of our system call in syscall.c file. We will write it in different file. Hence, we will add the function prototype in this file.

```c
extern int sys_get_name(void);
```

![[Pasted image 20240619200606.png]]

## 2.syscall.h 

There is array of function pointers in file syscall.c To index in this array , we will define number of system call in syscall.h file. This number is used for indexing in that array of function pointers.

```css
#define SYS_get_name 22
```

![[Pasted image 20240619200704.png]]

## 3.sysproc.c

We will implement our system call in this file.

```c
int sys_get_name(void){
	cprintf("This is tawheed --> ExcEpt_mE!");
	return 8;
}
```

![[Pasted image 20240619200812.png]]

This is basic implementation of system call. We are returning our roll number from system call. For doing something more, like passing arguments to sysetem call, refer other system calls written already in sysproc.c. Eg. for passing int as an argument to system all, refer “kill system call “.

## 4.usys.S

For user program to able to call this system call, interface need to be added. This interface is added in usys.S file. (extension for assembly files .S)

```c
SYSCALL(get_name)
```

![[Pasted image 20240619201031.png]]

## 5.user.h

Now, we need to add function prototype which user program will call. This is added in user.h file.

```c
int get_name(void);
```

![[Pasted image 20240619201341.png]]



This function is mapped to system call from the array of system call defined in file syscall.c with the index 22 which is defined in syscall.h.

Now, we have successfully added system call in xv6. We need to write small user program to call this system call.

***User Program named get_name.c :***

```c
#include "types.h"
#include "stat.h"
#include "user.h"

int main(void) {
	printf(1, "\nreturn val of system call is %d\n", get_name());
	exit();
}
```

One last step for running this user program, we need to modify the Makefile. Add the filename of user program without file extension in UPROGS section of Makefile.  
In Makefile,

![[Pasted image 20240619201409.png]]

Run xv6 & test your newly added system call.

```bash
make qemu-nox
```

```c
get_name
```

![[Pasted image 20240619201521.png]]
