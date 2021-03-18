# Prediction

<a href="http://oldblog.antirez.com/post/autocomplete-with-redis.html">Article</a>

## Problem

We want to auto complete based on most searched which hinders us in using the lexicographical auto complete.

## Solution

Every prefix is a sorted set containing all possible words to return. For example we have the words `news`, `new york`, `networth`, and `neanderthal`. The prefixes would be:

```
n
ne
nea
net
new
nean
neand
neande
neander
neandert
neanderth
neandertha
neanderthal
```

Imagine our prefix is `n`, then we would return the sorted set:

```
news
new york
networth
neanderthal
```

If our prefix would be `nea`, then we would return the sorted set:

```
neanderthal
```

With this approach we are able to sort in the prefix sorted sets and take advantages of the score by `ZINCRBY 1` a possible word when it got searched.
For example, if the word `networth` is searched a lot, so will the score of `networth` go higher in the sorted sets of `n` and `ne`, therefore it would be the first choice both if we use a `ZRANGE 0, 4` on it.

Here comes some drawbacks of this approach, which is that the prefix `n`, has possibly millions of words in its set, which is unnecessary for only displaying the top 5 results. We can limit the set with 300 by always removing the last element for a new search, so we have a big buffer, but not wasting a lot of space.
