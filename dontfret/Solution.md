Depending on where we are on the guitar we can play the same notes on a higher or lower string.

For each note we are given we can explore both up and down the strings by moving up/down 5 frets and checking
if we are in bounds both in terms of strings and frets.

The total ways we can play a tab requires some combinatorics. Each variation of a note we choose spans out to a tree of additional choices which
further span out into several more choices.

PseudoCode:

```

waysToPlayTab = 1

for note, string in tab {

    waysToPlayNote = 1
    waysToPlayNote += lowerStrings(note, string)
    waysToPlayNote += higherStrings(note, string)
    
    waysToPlayTab *= waysToPlayNote
}
```
