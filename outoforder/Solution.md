In this challenge we are told that there exists sequences of logs which can be traced from start to finish


Examples:

x1 -> x2 -> x3

y1 -> y2

z1 -> z2 -> z3 -> z4

However, the only way to find if a log is "connected" to another log is to perform some math and check
if the results match. Even if we find that two logs are connected such as 

z2 -> z3

We don't know if they are the beginning or the end of a sequence of logs.

We can arrive at a simple solution if we combine two techniques.

First of all we can create a lookup table for quickly finding a row given its continuation.
When we try to compute the next logrow in a sequence, we just have to check if such a row exists.


Java PseudoishCode 
```
public class LogRow {
    int continuation;
    int value;
    LogRow next;

    int nextContinuation() { return ((this.value % 52487) + (this.continuation % 52487)) % 52487; }

    int length() {
        int count = 0;
        for(LogRow row = this; row != null; row = row.next)
            count++;
        return count;
    }

    int continuationSum() {
        int sum = 0;
        for(LogRow row = this; row != null; row = row.next)
            sum += row.continuation;
        return sum;
    }
}

Map<Integer, LogRow> continuationLookup = new HashMap<>();

logs = parseLogRow(input)

logs.forEach(log -> continuationLookup.put(log.continuation, log))

// Builds a chain of logRows by linking them together

logs.forEach(log -> {
    if(continuationLookup.containsKey(log.nextContinuation())) {
        log.next = continuationLookup.get(log.nextContinuation());
    }
})


var longestSequence = continuationLookup.values().stream()
                                    .max(Comparator.comparingInt(LogRow::length)).orElseThrow();

var solution = longestSequence.continuationSum();
```