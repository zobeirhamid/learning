# Redis Learning: Hashes

<a href="https://www.youtube.com/watch?v=-agsJUihrWw">Video</a>

## Usage:

Collections of field-value pairs using strings as values, similar to JSON Object, Java HashMap, or Python Dictionary.

They are also mutuable, so you can:

- add
- change
- increment
- remove

## Commands

### Creating

```
HSET <key> <field1> <value1> <field2> <value2> ...
```

Returns the number of fields created.

#### Example

```
> HSET user:101 name Goku power 100 time-zone UTC-8
(integer) 2
```

### Change

```
HSET <key> <field1> <value1>
```

#### Example

```
> HSET user:101 time-zone PST
(integer) 1
```

### Delete

```
HDEL <key> <field>
```

#### Example

```
> HDEL user:101 time-zone
(integer) 1
```

### Retrieve

```
HGET <key> <field>
```

#### Example

```
> HGET user:101 power
"100"
```

### Retrieve All

```
HGETALL <key>
```

#### Example

```
> HGETAL user:101
1) "name"
2) "Goku"
3) "power"
4) "100"
```

### Numerical Manipulation

```
HINCRBY <key> <field> <value>
```

#### Example

```
> HINCRBY user:101 power -40
(integer) 60
```

## Time Complexity

### O(1)

- HSET
- HGET
- HDEL
- HINCRBY

### O(n) with n being the number of fields of the hash

- HGETALL
