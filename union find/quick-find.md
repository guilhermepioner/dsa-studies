# :books: Summary

1. [Quick Find](#quick-find)
    - [Data Structure](#data-structure)
      - [Find Implementation](#find-implementation)
      - [Union Implementation](#union-implementation)
    - [Java :coffee: Code](#java-coffee-implementation)
    - [Cost Model](#cost-model)
      - [Quick Find defect](#quick-find-defect)

# Quick Find

Quick Find is one possibile algorithm to solve the dynamic connectivity problem. It's commonly called an eager approach to solve it because it's slow.

## Data Structure

The Data Structure used to support the algorithm is simply an integer array of size *N* where the index are an object (index 3 means object 3, index 0 means object 0, etc...)

The only interpretation needed is that *p* and *q* are connected iff (***if and only if***) they have the same id (*index*)

Example of the array ***id[]***:

| *0* | *1* | *2* | *3* | *4* | *5* | *6* | *7* | *8* | *9* |
|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 1 | 8 | 8 | 0 | 0 | 1 | 8 | 8 |

> 0, 5 and 6 are connected <br>
> 1, 2 and 7 are connected <br>
> 3, 4, 8 and 9 are connected <br>

### Find implementation

With that in mind, for us to **Find** out if two objects *p* and *q* are connected, we just need to check if they have the same id

Using the same example of the array ***id[]*** above:

> id[6] = 0; id[1] = 1 <br> **6 and 1 are NOT connected** <br>
> id[0] = 0; id[8] = 8 <br> **0 and 8 are NOT connected** <br>
> id[5] = 0; id[6] = 0 <br> **5 and 6 ARE connected** <br>

### Union implementation

Union is a little bit harder in this model. In order to merge the components given two objects we need to **change ALL entries whose id is equal to one of them, to the other one**

> Rule: to merge componente containing *p* and *q*, change all entries whose id equal **id**[*p*] to **id**[*q*]
>
> **Arbitraryly, we choose to change the ones that are the same as *p* to the ones that are the same as *q***

Given the same array ***id[]*** as before, we will execute the union of 6 and 1:

| *0* | *1* | *2* | *3* | *4* | *5* | *6* | *7* | *8* | *9* |
|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 1 | 8 | 8 | 0 | 0 | 1 | 8 | 8 |
| ^ |   |   |   |   | ^ | ^ |   |   |   |

> Here we can understand the problem: *many values can change in a single operation*

Results in:

| *0* | *1* | *2* | *3* | *4* | *5* | *6* | *7* | *8* | *9* |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 1 | 1 | 8 | 8 | 1 | 1 | 1 | 8 | 8 |

> id[6] = 1; id[1] = 1 <br> **now 6 and 1 ARE connected** <br>

## Java :coffee: Implementation

```Java
// Creates QuickFind class to solve the Dynamic Connectivity problem
public class QuickFindUF 
{
  private int[] id;

  public QuickFindUF(int N)
  {
    id = new int[N];
    for (int i = 0; i < N; i++)
      id[i] = i // set id of each object to itself
  }

  public boolean connected(int p, int q)
  { return id[p] == id[q]; }

  public void union(int p, int q)
  {
    // Save values of the objects before chaning, possibly the whole array
    // Actually the maximum number of changes that can ocurr to the array id[] is N-1 
    int pid = id[p];
    int qid = id[q];

    for (int i = 0; i < id.length; i++)
      if (id[i] == pid) id[i] = qid;
  }
}
```

## Cost model

The cost model here is basically how many times we need to access the array (for read or write)

| algorithm | constructor | union | connected |
|----|-----|----|----|
| quick-find | N | N | 1 |

**order of growth of number of array accesses**

### Quick Find defect

The union of the Quick Find is too expensive, thus taking *N²* (*quadratic*) array accesses to process sequence of *N* union commands on *N* objects
