# Redis Learning: Strings

<a href="https://www.youtube.com/watch?v=n0LQREq4GrY">Video</a>

## Usage:

- Storing binary safe
  - String
  - Numerical Value
  - Serialized Json
  - Binary like image, sound, or video
- Caching combined with EXPIRE
  - API Responses
  - Session Storage
  - HTML Pages
- Counters - Manipulate numerical valeus

## Basic

### Storing

```
SET <key> <value>
```

#### Example

```
> SET user:101:time-zone UTC-8
OK
```

### Retrieve

```
GET <key>
```

#### Example

```
> GET user:101:time-zone
"UTC-8"
```

### Checking

```
EXISTS <key>
```

#### Example

```
> EXISTS user:101:time-zone
(integer) 0

> SET user:101:time-zone UTC-8
OK

> EXISTS user:101:time-zone
(integer) 1
```

## Caching

### Storing

```
SET <key> <value> EX <ttl>
```

#### Example

```
> SET usage:63 '{JSONobject}' EX 7200
OK
```

### Retrieving Expiration

```
TTL <key>
```

#### Example

```
> TTL usage:63
(integer) 7052
```

## Numerical Manipulation

### INCR

```
INCR <key>
```

Creates KEY if KEY does not exist.

#### Example

```
> EXISTS user:23:visit-count
(integer) 0
> INCR user:23:visit-count
(integer) 1
```

### INCRBY

```
INCBR <key> <number>
```

#### Example

```
> GET user:23:credit-balance
(integer) 40

> INCRBY user:23:credit-balance 30
(integer) 70

> INCRBY user:23:credit-balance -50
(integer) 20
```
