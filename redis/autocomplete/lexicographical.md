# Lexicographical

## Problem

We want to find out which words would come after the prefix `abc` but also including it, which would be `abc`, `abca`, `abcb`, `...`. There are different approaches in solving this problem.

## Solution 1

<a href="https://redislabs.com/ebook/part-2-core-concepts/chapter-6-application-components-in-redis/6-1-autocomplete/6-1-2-address-book-autocomplete/">Article</a>

We use a Redis Sorted Set and take advantage of the property when the score for all elements is `0` which is that the elements are sorted lexicographically. With that we can perform a `ZRANGE` between the starting element and the end element. Well, what are the starting element and the end element? The ending element is `abd`, but the starting element is unknown since `abzzzzzzzzzz...` is still before `abc`. But the element after `z` is `{`, so we could define the starting element as `ab{` and the ending element as `abc{`. We insert `ab{` and `abc{` using `ZSET`, find their respective position with `ZRANK` and do a `ZRANGE` between those two positions. With that we get all the elements which satisfy the prefix.

## Solution 2

<a href="http://oldblog.antirez.com/post/autocomplete-with-redis.html">Article</a>

The second solution is, we take all the possible solutions, and add their prefix into the sorted set, and mark the solutions with some character, like `*`. If we have the words `foo`, `bar`, and `foobar`, we would have to add the following elements also in the sorted set: `f`, `fo`, `b`, `ba`, `foob`, and `fooba`. We add the real words like this: `foo*`, `bar*`, and `foobar*`.
The structure would look like this:

```
b
ba
bar*
f
fo
foo*
foob
fooba
foobar*
```

If our prefix is `fo`, we would use `ZRANK` to get the position of `fo`, then perform a `ZRANGE` using that position and use some arbitary larger number like `50` as the limit. Then we would return those elements, and with a programming language we would only return the word `foo` and `foobar` since they are marked with a `*`.
