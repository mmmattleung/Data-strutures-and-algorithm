# Efficiency

## Introduction

Complexity is how well you're using your computer's resources to get a particular job done.It contains space and time.



## Quantifying efficiency

### Linear relationship

As the input increases, the number of lines executed increases by a proportional amount.

> As the input to an algorithm increases, the time required to run the algorithm may also increase.



The number of operations will be n^2*n*2. This is what we would call a **quadratic** rate of increase.

> As the input to an algorithm increases, the time required to run the algorithm may also increase—and different algorithms may increase at different rates.



### Order

> *The* *rate of increase* *of an algorithm is also referred to as the* ***order*** of the algorithm.



For example, instead of saying "this relationship has a linear rate of increase", we could instead say, "the *order* of this relationship is linear", and it marks as Big O.



### Big O Notation

#### Basic

It's a form to descrip the efficiency of algorithm.Such as O(0n + 1), O(n), O(n^2), O(log n), O(n log n) etc.

And the "n" refer to the length of the input to your algorithm.



#### Complication

For higher level computer language, such as Python 'for' loop, it may be a few lines of code, but it would be doing a lot more in the background.And different types of data structures will effect the efficiency.



#### Approximation

In fact, most of time, we care a lot whether the algorithm's increasing ratio of time complexity in approximation.

`````
Such as O(12n+5), O(30n), O(2n+10) are about O(n).
In the interview your can say, "Some number of computations must be performed for each letter in the input" to explain the thinking.
`````



####s The Worst Case

We are foucs on the worst case beacuse it puts on upper bound on the amout of time our code is going to take.And we can talk about efficiency in terms of the average case or even best case.



#### Space efficiency

It's how efficiency our algorithm is in terms of memory usage.