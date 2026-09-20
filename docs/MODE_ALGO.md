# Mode Algorithm Explanation

So, I found out that R's standard library does not have a `mode()` function to calculate the mode of a column in a dataframe, or an array of elements. So, I honestly asked Claude: what is the best way to calculate the mode, and it retrieved this algorithm:

```r
ux <- unique(x)
ux[which.max(tabulate(match(x, ux)))]
```

I was confused to say the least, since I was just acquainted with R. I probably should've followed the path of laziness and installed another package with the actual function, but I decided to be YAGNI instead. So, I'll explain what's going on.

So, first of all, let's say that we have a vector `x` where we have stored a sample of values:
`x <- c(1, 2, 2, 6, 2, 4, 1, 2, 2, 4, 4, 6, 4, 6)`

At first glance, we can tell that the mode is 2, but our computer is dumb, and it doesn't know, so we must find a solution to finding the mode algorithmically.

First, let's get rid of our duplicated values. Why? You'll see, just trust me.

`ux <- unique(x)`

We should be left with the following list:

`(1, 2, 6, 4)`

This list has all the values that exist in `x`, which is great.

`match(x, ux)`

What this will do is exactly this: where does each value of my original list fall in my list of unique values? And so the match function runs through both, compares, and tells us where they fall:

```r
1 -> 1
2 -> 2
2 -> 2
6 -> 3
...
4 -> 4
6 -> 3
```

And we get this list (hoping that I didn't mess up while typing):

`1, 2, 2, 3, 2, 4, 1, 2, 2, 4, 4, 3, 4, 3`

Now, we'll calculate the frequency of each index, by using the `tabulate()` function, and we'll get something like this:

`(2, 5, 3, 4)`

Now, this is where it gets interesting. Look at our unique values array, and the array obtained with tabulate!

```r
(1, 2, 6, 4)
(2, 5, 3, 4)
```

We just got which is the frequency of the unique values in the original list! Just by knowing how much did each index repeat.

And now we ask the computer: which one is the maximum value in our array?

`which.max(2, 5, 3, 4)`

Well, obviously the argument at position 2! So, our mode is...

`uniques[2] = 2`

Yay!