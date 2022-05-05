In this question we need to figure out the optimal path from one side to another.
Because we have multiple entry and exit points, this can be expensive.

Using an algorithm such as Djikstra can give us the shortest path relatively cheap
but since there are a lot of iterations and a lot of options per iteration this becomes expensive.

A "trick" we can use is to look at the challenge differently.

This is what we are given, multiple entry and exit points.


A - # - # - # - B
    |   |   |
A - # - # - # - B
    |   |   |
A - # - # - # - B
    |   |   |
A - # - # - # - B


However there is nothing that stops us from creating an additional extra node on each side
and give it a cost of 0. Now if we apply Djikstras algorithm to find the path between the 2 extra nodes
we automatically find the best exit and entry points.

        # - # - #
      / |   |   | \
A - # - # - # - # - # - B
     \  |   |   | / 
        # - # - # 
