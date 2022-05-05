There are several ways to solve this question but this was my approach

One way is to traverse each "height" level of the ship one level at a time starting from the bottom.
By height level I mean the height level of how many containers are stacked ontop of each other. 

We can start at level 0 and visit each cell ( will refer to containers as cell from now on ) in the grid. From each container we can try to find a way to the edge of the ship using a graph traversal algorithm such as DFS/BFS. If there is a path to the edge of the ship, then this cell and every other cell that was traversed in this traversal can't trap water since any water that falls on these containers would spill of the side.

We can mark every cell that connects to the side of the ship as "leaking" or similar. That was if we ever touch a cell
that "leaks" while on the same or a higher level, we know that every cell reachable from this cell must also be leaking.

If a path we explored does not touch a cell that "leaks" or reaches the side of the ship, then this path forms a lake which traps water ( on this level and on any lower levels ). How much water it can trap depends on how high the surronding walls are. As we traverse the lake we can update each cell to tell how much water this cell holds.


Consider the following illustrated example where water is trapped on level 1 and on level 2.
As we traverse level 1 we will mark that the cell with cordinate (1,1) traps 1 unit of water.

When we traverse level 2, we update the cells watermark to 2 units of water. We can update it as follows

waterLevel of a cell = Max( current cell water level,  current levels lake border height - cell height)



Side View
```

    ┌──┐     ┌──┐
 2  │  │xxxxx│  │
    ├──┤xx┌──┼──┤
 1  │  │xx│  │  │
    ├──┼──┼──┼──┤
 0  │  │  │  │  │
    └──┴──┴──┴──┘
```



Top View

```
3 3 3
3 1 3
3 2 3
3 3 3
```

As we traverse from level 0 all the way to the highest container, we will have marked all cells as either leaking
and or how much water it traps. The total amount of trapped water can then be found by summing up all cells that trap water.



Very Simplified PseudeCode

```
for level from  0 -> tallest container {

    for cell in grid {

        path = tryFindPathToEdgeOfShip(cell)

        if path does not form Lake {
            for cell in path {
                cell.leaks()
            }
        } else {
            for cell in path {
                cell.updateWaterLevel()
            }
        }
    }
    sumOfWater = cellWithWater.sum()
}
