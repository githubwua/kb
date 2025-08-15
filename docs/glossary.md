# multimap

A multimap is a collection of key/value pairs where a single key can be associated with multiple values.
For example,

* Standard Map: `{"Alex": "555-1234"}`
* Multimap: `{"Alex": ["555-1234", "555-5678", "555-9999"]}`

The phrase "The input to `GroupByKey` is a collection of key/value pairs that represents a multimap" means you start with a flat list of key/value pairs where keys are duplicated. 
The job of `GroupByKey` is to process this list and create an actual multimap structure.

Essentially, `GroupByKey` is the operation that **groups** all values for the same key together into a list or collection.

## Example

Imagine you have the following collection of key-value pairs as your **input**. This *flat* list represents a multimap because the keys `apple` and `banana` appear more than once.

```
("apple", 1)
("banana", 1)
("apple", 1)
("cherry", 1)
("banana", 1)
("apple", 1)
```

After you apply the **`GroupByKey`** operation, you get this **output**, which is a true multimap structure:

```
("apple",  [1, 1, 1])
("banana", [1, 1])
("cherry", [1])
```

So, `GroupByKey` takes a list that conceptually represents a multimap and transforms it into an explicit multimap structure, where each key is paired with an iterable (like a list) of all its associated values.