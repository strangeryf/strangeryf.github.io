---
layout: post
title:  "MSDN made a blunder"
date:   2006-01-10
tags: MSDN 
---
Have a look at this URL: http://msdn.microsoft.com/library/default.asp?url=/library/en-us/vccore98/html/_crt_a_sample_generic.2d.text_program.asp. Anything wrong? Well, it’s not easy to find. But after you complie and run the C source files, you may get a message box saying that something is wrong and the application will close, etc. What’s wrong with the source? If you use an MS IDE, you may find that the code breaks at somewhere of the CRT source files, which are provided by MS itself. What makes things strange is, if you use a visual studio command console, and use cl (without any options) to compile those source files, the code runs and the result is correct! But if you use gcc(mingw32), you will get the same results as you get in the IDE. In fact, the CRT functions xxxrev(INPUT_STRING_POINTER) needs the passed in pointer to be a pointer pointing to some place where can be overwritten. But MSDN uses a char(or wchar_t) pointer that points to a constant string that can never be overwritten. So you got the error. Let’s review some fragments of those codes:
```c
    char *str = "Astring"; char *amsg = "Reversed";
    printf("’%s’\n", strrev(str));
```
Here, strrev requires the input parameter to be a pointer to a writable memory, BUT str points to a string literal, and we will have that ugly error. To correct this, just use a char-array like this: 
```c
    char str[8] = "Astring";
    char *str1 = str;
    printf("’%s’\n", strrev(str));
```