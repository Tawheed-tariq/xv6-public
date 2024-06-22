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

![image](https://github.com/Tawheed-tariq/xv6-public/assets/143424182/da0f08d7-7626-46a7-9c8e-c1dd020936af)


One more change is to be done in this file.  
We are not going to write implementation of our system call in syscall.c file. We will write it in different file. Hence, we will add the function prototype in this file.

```c
extern int sys_get_name(void);
```

![image](https://github.com/Tawheed-tariq/xv6-public/assets/143424182/c7ec484d-fbc9-41bc-a9d4-f8e8fe99d7f9)


## 2.syscall.h 

There is array of function pointers in file syscall.c To index in this array , we will define number of system call in syscall.h file. This number is used for indexing in that array of function pointers.

```css
#define SYS_get_name 22
```

![image](https://github.com/Tawheed-tariq/xv6-public/assets/143424182/1e8f4d22-a828-434a-ad06-7eb45c3eb979)


## 3.sysproc.c

We will implement our system call in this file.

```c
int sys_get_name(void){
	cprintf("This is tawheed --> ExcEpt_mE!");
	return 8;
}
```

![image](https://github.com/Tawheed-tariq/xv6-public/assets/143424182/d0927b5b-bbcc-47d8-8a2e-9efdd71510ac)


This is basic implementation of system call. We are returning our roll number from system call. For doing something more, like passing arguments to sysetem call, refer other system calls written already in sysproc.c. Eg. for passing int as an argument to system all, refer “kill system call “.

## 4.usys.S

For user program to able to call this system call, interface need to be added. This interface is added in usys.S file. (extension for assembly files .S)

```c
SYSCALL(get_name)
```

![image](https://github.com/Tawheed-tariq/xv6-public/assets/143424182/5948f337-8bca-45bc-b0b1-f86836cb1335)


## 5.user.h

Now, we need to add function prototype which user program will call. This is added in user.h file.

```c
int get_name(void);
```

![image](https://github.com/Tawheed-tariq/xv6-public/assets/143424182/3eb1c6f7-e5cc-4a18-a23d-5ec7bf0654b4)




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

![image](https://github.com/Tawheed-tariq/xv6-public/assets/143424182/0d7926e5-1bcf-4481-8411-524abf9a4677)


Run xv6 & test your newly added system call.

```bash
make qemu-nox
```

```c
get_name
```

![image](https://github.com/Tawheed-tariq/xv6-public/assets/143424182/d1cb3435-4480-404f-a4c1-4356477e3e52)

