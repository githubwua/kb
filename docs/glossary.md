
# groupbykey

GroupByKey represents a transform from a *flat multimap* (multiple keys to individual values) to a *nested uni-map* (unique keys to collections of values).
For example, as input, we have words from a text file and the line number on which they appear. 

Input (a flat list): 
```
cat, 1
dog, 5
and, 1
jump, 3
tree, 2
cat, 5
dog, 2
and, 2
cat, 9
and, 6
```

We want to group together all the line numbers (values) that share the same word (key), letting us see all the places in the text where a particular word appears.
GroupByKey gathers up all the values with the same key and outputs a new pair consisting of the unique key and a collection of all of the values that were associated with that key in the input collection. 

Output (a nested list):
```
cat, [1,5,9]
dog, [5,2]
and, [1,2,6]
jump, [3]
tree, [2]
```

GroupByKey is a good way to aggregate data that has something in common. For example, if you have a collection that stores records of customer orders, you might want to group together all the orders from the same postal code (wherein the “key” of the key/value pair is the postal code field, and the “value” is the remainder of the record).

Ref: 
[GroupByKey](https://beam.apache.org/documentation/programming-guide/#groupbykey)


# multimap

See [groupbykey](#groupbykey)
