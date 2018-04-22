---
layout: post
title:  "Look up a dictionary"
date:   2006-02-28
tags: C++
---
There is a dictionary file located at /usr/share/dict/linux.words, I would like to test this with some searching algorithms. To my surprise, this file is not alphabetically organized, then I let Notepad++ sort that file and save that as "words" so that I can use a binary searching method. Also, I use a set in STL to deal with the original file.

*rdtsc.h*
```cpp
/* I dislike the current implementation of inline
both in ms C(except for C++) and gcc(C&C++), so
I use the "define" macro here.
Input should be of type "unsigned long long" */
/* ReaD TimeStamp Counter, for Pentium & above only
msc don’t support C99 keyword inline! */
#if defined _MSC_VER
#define rdtsc(tsc) \
    __asm rdtsc \
    __asm mov dword ptr [tsc], eax \
    __asm mov dword ptr [tsc+4], edx
#elif defined __GNUC__
/*
The movl instruction expands to 2 instructions
movl %eax, 4(%esp)
movl %edx, 8(%esp)
"=A" only used in IA-32 arch
ref: gcc manul(v4.0.2)
5.35.4 Constraints for Particular Machines*/
#define rdtsc(tsc) \
    asm ("rdtsc;" \
    "movl %%eax, %0" : "=A"(tsc))
#endif
```

*timing.h*
```cpp
#include <time.h>
#ifdef __cplusplus
extern "C"
{
#endif
    /* Pauses for a specified number
of milliseconds(Windows) or microseconds(Linux) */
    void slp(clock_t wait);
    /************************************************
* Time counting not exact *
* because priority not raised to top *
*************************************************/
    /* Get CPU frequency */
    double GetCPUFreq();
#ifdef __cplusplus
}
#endif
```

*timing.c*
```c
#include <time.h>
#include "rdtsc.h"

/* Pauses for a specified number of
millisecs(Windows) or microsecs(Linux)*/
void slp(clock_t wait)
{
    clock_t goal;
    goal = wait + clock();
    while (goal > clock());
}

/************************************************
* Get CPU frequency *
* Do not use gcc -O to complie this function! *
* Time counting not exact *
* because priority not raised to top *
*************************************************/
double GetCPUFreq()
{
    volatile unsigned long long t0, t1;
    double cpu_freq;

    slp(CLOCKS_PER_SEC / 100);
    rdtsc(t0);
    slp(CLOCKS_PER_SEC * 1);// iterval should within
    rdtsc(t1);

    cpu_freq = (t1 - t0) * 1.0;
    return cpu_freq;
}
```

*dict.cpp*
```cpp
/***********************************************
* find_word — find a word in the dictionary. *
* binary searching *
* Usage: *
* find_word <word-start> [<word-start>…] *
************************************************/
#include <iostream>
#include <fstream>
#include <iomanip>
#include <cstdlib>
#include <ctime>
#include "rdtsc.h"
#include "timing.h"

// Binary search
int binsearch(char **dict, int len, const char *str)
{
    int low = 0, high = len - 1, mid, cmp;
    while (low <= high)
    {
        mid = (low+high)/2;
        cmp = strcmp(str, dict[mid]);
        if (cmp == 0)
            return mid;
        if (cmp < 0)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return -1;
}

int main(int argc, char *argv[])
{
    using namespace std;

    int i = 0;// dictionary length conter
    int index;// the found index in the dictionary
    ifstream dict_file("words");// The dictionary to search
    char **words, buf[50];// string array to store words
    unsigned long long t0, t1;// timer
    double elapsed;// time elapsed

    words = new char*[500000];

    cout.precision(1);

    cout << "Calculating CPU frequency…\n";
    const double cpu_freq = GetCPUFreq();
    cout << "Currenct CPU frequncy is " << fixed
    << cpu_freq/1000000 << " MHz\n";

    if (!dict_file)
    {
        cerr << "Error: Unable to open "
        "dictionary file\n";
        exit(1);
    }

    // Read the dictionary and construct the 2-d array
    cout << "Building dictinary array…\n";
    rdtsc(t0);
    while (1)
    {
        dict_file.getline(buf, 50);
        if (dict_file.eof())
            break;
        words[i] = new char[sizeof(buf)+1];
        strcpy(words[i], buf);
        i++;
        if (i>500000)
        {
            cerr << "Too many words\n";
            exit(1);
        }
    }
    rdtsc(t1);
    elapsed = (t1 - t0) / cpu_freq;
    cout << "Dictionary built in " << fixed << elapsed
    << " s!\nDictionary size is " << i << " words";

    // Look up each word
    while (argc > 1)
    {
        cout << "\nLooking up \"" << argv[1] << "\"…\n";
        rdtsc(t0);
        index = binsearch(words, i, argv[1]);
        rdtsc(t1);
        elapsed = (t1 - t0) / cpu_freq * 1000000;
        if (index > 0)
            cout << "===> Found \"" << words[index] << "\" in "
            << fixed << elapsed << " us";
        else
            cerr << "===>" << argv[1] << " not found!\n";
        ++argv;
        -argc;
    }

    // Do some gc
    for (i=i-1; i>=0; i-)
    delete[] words[i];
    delete[] words;
}
```

*setdict.cpp*
```c
#include <iostream>
#include <fstream>
#include <string>
#include <set>
#include "timing.h"
#include "rdtsc.h"

int main(int argc, char *argv[])
{
    using namespace std;

    unsigned long long t0, t1;
    double elapsed;
    string s;
    set<string> dict_set;
    set<string>::iterator dict_itr;
    ifstream dict_file("linux.words");

    if (!dict_file)
    {
        cerr << "Can’t open file\n!";
        abort();
    }

    const double cpu_freq = GetCPUFreq();
    cout << "Currenct CPU frequncy is " << fixed
    << cpu_freq/1000000 << " MHz\n";

    // Read the dictionary and construct the set
    cout << "Building dictionary set…\n";
    rdtsc(t0);
    while (getline(dict_file, s))
    {
        dict_set.insert(s);
    }
    rdtsc(t1);
    elapsed = (t1 - t0) / cpu_freq;
    cout << "Dictionary built in " << elapsed << " s!\n"
    << "Dictionary size is " << dict_set.size() << " words";

    // Look up each word
    while (argc > 1)
    {
        cout << "\nLooking up \"" << argv[1] << "\"…\n";
        rdtsc(t0);
        dict_itr = dict_set.find(argv[1]);
        rdtsc(t1);
        elapsed = (t1 - t0) / cpu_freq * 1000000;
        if (dict_itr != dict_set.end())
            cout << "===>Found \"" << *dict_itr <<"\" in "
            << elapsed << " us";
        else
            cerr << argv[1] << " not found!";
        ++argv;
        -argc;
    }
}
```