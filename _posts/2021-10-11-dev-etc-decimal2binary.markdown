---
layout: post
title:  "[Computer Science] Decimal to binary conversion"
subtitle:   "2to10"
categories: dev
tags: dev etc   
comments: true
---


## Summary
> How to convert decimal to binary
  
- Index
    - [Separate sign and absolute](#Separate-sign-and-absolute) 
    - [Convert the integer part](#Convert-the-integer-part)
    - [Convert the fractional part](#Convert-the-fractional-part)
    - [Result](#Result)


## Separate sign and absolute

Example Decimal Number = 24.3125

24.25 = 24 + 0.3125

## Convert the integer part
```
24 / 2 = 12
```

remainder = **0**

```
12 / 2 = 6
```

remainder = **0**

```
6 / 2 = 3
```

remainder = **0**

```
3 / 2 = 1
```

remainder = **1**

```
1 / 2 = 0
```

remainder = **1**

```
24(10) = 11000(2)
```

## Convert the fractional part

```
0.3125 x 2 = 0.625
```

greater than 1? -> no (**0**)

```
0.625 x 2 = 1.25
```

greater than 1? -> yes (**1**)

1.25 - 1 = 0.25

```
0.25 x 2 = 0.5
```

greater than 1? -> no (**0**)

```
0.5 x 2 = 1
```

equal to 1? -> yes (**1**)

stop

```
0.3125(10) = 0.0101(2)
```

## Result

```
24.3125(10) = 11000.0101(2)
```
