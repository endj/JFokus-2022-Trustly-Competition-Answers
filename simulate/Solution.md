We can either build a permutation tree with all combinations 
of possible characters or we can use math to figure out the answer.
Not much to this question other then making fun of Metaverse.


Java Code

Math solution
```
int sum = 1
for(var c : name.toLowerCase().toCharArray()) {

    if(c == 'i' || c == 'l' || c == 'o')
        sum *= 3;
    else
        sum '= 2;
}
return sum
```