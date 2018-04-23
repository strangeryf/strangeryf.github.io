---
layout: post
title:  "Trailing zeros of factorial"
date:   2009-06-10
tags: puzzle algorithm
---
A friend of mine talked about a classic number puzzle in a chat room. The puzzle is how many trailing zeros are there in the factorial of 100. He was writing some C code and getting into troubles. It is such a simple puzzle that even a pupil can work it out in minutes. His solution is quick and simple:
```c
for (i=5; i<=100; i+=5)
{
    t = i;
    while (t%5 == 0)
    {
        count++;
        t /= 5;
    }
}
```
Just counting the factor 5 in multiples of 5, because we have plenty of multiples of 2 which will make a 10 with factor 5.

It is reminiscent of the BigDecimal class in Java, which leads to a brutal or straightforward way of solving it.
```java
BigDecimal a, b;
a = new BigDecimal(2);
for (i=3; i<=100; i++) {
    b = new BigDecimal(i);
    a = a.multiply(b);
}
String result = a.toString();
Pattern p = Pattern.compile("0+$");
Matcher m = p.matcher(result);
if (m.find()) {...}
```
In fact, there is a formula that counts the trailing zeros: n/5+n/5^2+n/5^3+… Here, "/" is the floor of the division. That is
```c
for (i = 5; i<=N; i*=5)
    count += N/i;
```
Very easy to understand, isn’t it?
