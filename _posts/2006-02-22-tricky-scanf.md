---
layout: post
title:  "Tricky scanf"
date:   2006-02-22
tags: C scanf
---
The infamous scanf is used in the following calculator, but the simple "while(…getch()…)" patch does not work. After patch the "if (scanf(…)==2)", I got more trouble when entering unexpected strings: the "Bad…" something will appear over and over.
```c
/************************************************
 * calc — Simple 4 function calculator.        *
 *                                              *
 * Usage:                                       *
 *      $ calc                                  *
 *      Enter operator and value: + 5           *
 *                                              *
 * At the end of each operation the acculated   *
 * results are printed.                         *
 ************************************************/
#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
int main() {
    char oper;  /* Operator for our calculator */
    int  result;/* Current result */
    int value;  /* Value for the operation */
    char buf[2];  /* temporary buffer */

    result = 0;
    while (1)
    {
        printf("Enter operator and value:");

        if (scanf("%c %d", &oper, &value) == 2)
            fgets(buf, 2, stdin);

        switch (oper) {
            case '+':
                result += value;
                break;
            case '-':
                result -= value;
                break;
            case '*':
                result *= value;
                break;
            case '/':
                if (value == 0)
                    printf("Divide by 0 error\n");
                else
                    result /= value;
                break;
            case 'q':
                exit (0);
            default:
                printf("Bad operator entered\n"); break;
        }
        printf("Total: %d\n", result);
    }
}
```
On known solution is using fgets and sscanf instead of scanf:
```c
    char line[SOME_SIZE];
    fgets(line, sizeof(line), stdin);
    sscanf(line, "%c %d", &oper, &value);
```
Else? Don't know :)