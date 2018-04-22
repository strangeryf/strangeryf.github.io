---
layout: post
title:  "Notes on Oualline's book"
date:   2006-12-19
tags: C++
---
In 2003, Oualline published his book – How Not to Program in C++. It is an interesting book, and you will find you have to worry about compilers and assembly instructions. I have recently worked out some notes on it, enjoy.

//
// The following is the offcial errata
//

Program #13, Lines #25 & #27
‘endl’ is in std namespace, so both lines should read ...<< std::endl;
 
Program #19, Line #19
"default" should be "defualt" (should be misspelled)
 
Program #43, line #35
should be "class der: public base"
 
Program #44, line #32
should be "while (array[i] != -1)"
 
Program #46, line #56
should be "cur_cmd->cmd != NULL)"

Answer #57, first code
"20" should be "21"
 
Answer #70, line #56
should be "cur_cmd->cmd != NULL)"

//
// The following is my notes
//

Program #46, line #60
should be "if (cur_cmd->cmd == NULL) {"

Program #47, line #29
should be "if (!in_file)"

Program #53
in fact, nothing goes wrong, we can return a reference to a parameter

Program #85
do not forget to free memory in the dtor

Program #86, line #75
should be "array& to_array,"
line #84
should be "to_array[12] = 5;"

Answer 75,
should be
```cpp
    if (this != &old_array)
    {
        ...       
    }
    return (*this);
```

Program #88, line #10
missing a "/" at the end

Attention!

Program #89
The function call flow of VC differs from that of gcc. Because the operator + returns an object, the copy ctor may or may not be invoked.

Program #94
(Memory pool?)The program will run normally, and no memory leak will happen. But the array logic is wrong.

Program #99, line #13 should be
    if (access("delete.me", F_OK)==0)
Ref:
```
ACCESS(2)                  Linux Programmer’s Manual                 ACCESS(2)

NAME
       access – check user’s permissions for a file

SYNOPSIS
       #include <unistd.h>

       int access(const char *pathname, int mode);

DESCRIPTION

access()  checks  whether  the process would be allowed to read, write or test for exis-
       tence of the file (or other file system object) whose name is pathname.  If pathname  is
       a symbolic link permissions of the file referred to by this symbolic link are tested.

       mode is a mask consisting of one or more of R_OK, W_OK, X_OK and F_OK.

       R_OK,  W_OK  and  X_OK  request checking whether the file exists and has read, write and
       execute permissions, respectively.  F_OK just requests checking for the existence of the
       file.

RETURN VALUE
       On  success  (all  requested permissions granted), zero is returned.  On error (at least
       one bit in mode asked for a permission that is denied, or some other error occurred), -1
       is returned, and errno is set appropriately.
```

Progam #100, Note:
use the C99 offsetof macro instead of the strange OFFSET macro

Program #111,  line #95
    "&reader_hread" should be "&reader_thread"
Be sure to compile with "-lpthread" option
->Steps of using mutex in pthread:
1. Declare an object of type pthread_mutex_t.
1. Initialize the object by calling pthread_mutex_init().
1. Call pthread_mutex_lock() to gain exclusive access to the shared data object.
1. Call pthread mutex unlock() to release the exclusive access and allow another thread to use the shared data object.
1. Get rid of the object by calling pthread_mutex_destroy().
