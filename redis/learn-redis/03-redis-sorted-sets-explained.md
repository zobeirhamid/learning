# Redis Learning: Hashes

<a href="https://www.youtube.com/watch?v=XqSK-4oEoAc">Video</a>

## Usage:

- Ordered collection of unique values
- Each member has an associated score
- Can be accessed in ascending or descending order
- Scores in sets can be incremented or decremented

## Commands

### Adding

```
ZADD <key> <score> <member>
```

#### Example

```
> ZADD leaders:exp 0 42
(integer) 1

> ZADD leaders:exp 0 391
                   0 127
(integer) 2
```

### Manipulation

```
ZINCRBY <key> <value> <member>
```

#### Example

```
> ZINCRBY leaders:exp 300 42
"300"
```

### Retrieving in ascending order

```
ZRANGE <key> [<offset> <limit> WITHSCORES]
```

#### Example

```
> ZRANGE leaders:exp 0 1 WITHSCORES
1) "127"
2) "0"
3) "391"
4) "0"
```

### Retrieving in descending order

```
ZREVRANGE <key> [<offset> <limit> WITHSCORES]
```

#### Example

```
> ZREVRANGE leaders:exp 0 1 WITHSCORES
1) "42"
2) "300"
3) "391"
4) "0"
```

### Retrieve position

```
ZRANK <key> <member>
```

starting from 0.

#### Example

```
> ZRANK leaders:exp 42
(integer) 2
```

### Retrieve position in reverse order

```
ZREVRANK <key> <member>
```

starting from 0.

#### Example

```
> ZEVRANK leaders:exp 42
(integer) 0
```

### Retrieve score

```
ZSCORE <key> <member>
```

#### Example

```
> ZSCORE leaders:exp 42
"300"
```
