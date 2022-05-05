In this question we have a program with functions which can call other functions.

In order to figure out the total number of calls, we can go function by function
and count how many function calls are made. This involves recursively following each function call
since functions can call other functions.

A small optimisation we can do in this case is to store the number of functions a call will make in a lookup table
once we figure it out. This way, the next time we encounter a function we have invoked before, we don't have to follow 
the chain of functions since we have already computed how many invocations that would result in.

Pseudo Code

```
functionCountMap = Map()

explore(function) {
    subcalls = 0

    if functionCountMap[function] explored {
        return functionCountMap[function]
    }
    
    for subfunction in function {
        subCalls += explore(subfunction)
    }

    functionCountMap[function] = subcalls + 1
    
    return calls
}

totalCalls = 0

for function in program {
    totalCalls += explore(function)
}

```