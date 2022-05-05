There is nothing really special about solving this question as long as we follow the examples.

There is a small trick we can apply to save space though.

Instead of having 1 entry to keep track of patience for each individual investor.
We can have 1 entry for each day. The number at each index indicates the number of investors with that many days of patience left.

When we add a new investor to our project, we just increment the 25th index in our array.

Every day we can just shuffle our array 1 step to the left to indicate investors loosing patience.
To get the valuation of the coin we can just sum up the counts of the array.

