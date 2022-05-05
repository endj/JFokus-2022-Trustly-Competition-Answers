In this question we need to count a large number of blocks in a pyramid where some blocks have been removed.

The first solution that might come to mind would be to allocate a 2d array the same size as the pyramid,
go round and round layer by layer and write down the heights at each cell. Afterwards, we just need to
sum up each cell in the grid minus the layers that should be removed.

If we try to allocate the array we will probably run out of memory. We can just use the same approach but without
memory, summing up the counts as we go.

Another non-obvious solution is to use the fact that the pyramid is increasing in height 1 block at a time.
This might get us to think of the series of natural numbers 1 + 2 + 3 .. 

If we can exploit this somehow, we can use the formula n(n + 1) / 2 to count the number of blocks up to n starting from 1.
However, even if we could slice a pyramid in such a way to exploit this, there are other challenges.


Let's look at a pyramid from the side. There are 2 variations based on the length of the sides.

odd length side view

```
     #
   # # #
 # # # # #
```

even length side view

```
    # #
  # # # #
# # # # # #
```

In order to get countable slices, we can split the pyramid up in 2 parts 

Odd case:

Here we can't split it up evenly so we will end up duplicating the middle. 
We will have to account for this so we don't end up double counting
```
    #     #
  # #     # #
# # #     # # #
```


Even case:

Pyramid split in 2 clean parts
``` 
    #    #
  # #    # #
# # #    # # #
```

Now each slice can be summed up quickly.
```
    #
  # #
# # #
1 2 3
```
3(3 + 1) / 2 = 6

However, not every slice has the same length

Consider the top view, where can we apply the formula?


```
1 1 1 1 1
1 2 2 2 1
1 2 3 2 1
1 2 2 2 1
1 1 1 1 1
```

Consider breaking out a quarter of the pyramid. We can now apply the formula to each quarter by applying it
to each row which is now increasing.


```
1
1 2
1 2 3
1 2 
1
```

We can even optimize this further by only doing half a quarter and doubling the result.

```
1
1 2
1 2 3
```

However, at every step we need to be careful because some parts get double counted.
This includes the diagonals, the middles and even the center of the pyramid.

Once we have the sum of a quarter, we know that 4 quarters makes a whole.

Pseudo Code

```
quartersSummed = blocksInQuarter() * 4

if pyramidLength is even {
    result = quartersSummed - doubleCountedDiagonal()
} 

if pyramidLength is odd {
    result = quartersSummed - doubleCountedDiagonal() - doubleCountedCenter()
}
```

The exact calculations are slightly tricky but you can work them out on paper. 
