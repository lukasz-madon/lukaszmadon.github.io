---
layout: post
title: Sum bitdiff between all pairs of numbers in a collection
date: 2013-06-24 20:26:32.000000000 +00:00
categories:
- Java
tags:
- java
- algorithm
- interview
---
There are many ways to compare two integers. One of them is to compare each bit of numbers e.g. comparing 2 and 1:

    2 -> ...0010
    1 -> ...0001
 
Two last bits are different, so the result is 2. Here is one of many possible implementations:       

```java
        public static int bitDiff(int a, int b)
        {
            int count = 0;
            for (int i = 0; i < 32; i++)
            {
                int aBit = (1 << i) & a;
                int bBit = (1 << i) & b;
                if (aBit != bBit)
                {
                    count++;
                }
            }
            return count;
        }
```

Now let's have a look at more complex problem. From a collection of integers calculate bitDiff of all pairs and then sum the results.

 &#8721; bitDiff(array[i], array[j])

```
    input: {1,2,3} -> pairs {(1,2),(1,3),(2,1),(2,3),(3,1),(3,2)} -> output: 8
```

This can be optimized by generating just half of the pairs (bitDiff operation is transitive), but it's still O(n^2). Can we do O(n)? Scroll for a hint!

<br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/>

What if we just have 0's and 1's in the array?

<br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/>

Let's consider a simple case:

    [0,1] ->  1
    [1,1] ->  0
    [0,0] ->  0
    [1,0] ->  1

Clearly, the result is 1 for pairs that are different. We can count 1's and 0's and multiply each other to get the number of pairs that result is 1 and then multiply by 2 (permutation of a pair)

    [0,1] = 1 * 1 * 2 = 2
    [0,1,1] = 1 * 2 * 2 = 4
    [0,1,0,1] = 2 * 2 * 2 = 8

How to get the generalization for ints?

We can threat numbers as 32 arrays of 1's and 0's

```java
        public static bool isBitSet(int number, int index)
        {
            int bit = (1 << index) & number;
            return bit > 0;
        }

        public static int sumPairBitDiff(int[] numbers)
        {
            int sum = 0;
            for (int i = 0; i < 32; i++)
            {
                int oneCount = 0;
                int zeroCount = 0;
                foreach (var num in numbers)
                {
                    if (isBitSet(num, i)) oneCount++;
                }
                zeroCount = numbers.Length - oneCount;
                sum += oneCount * zeroCount * 2;
            }
            return sum;
        }
```

Awesome!


