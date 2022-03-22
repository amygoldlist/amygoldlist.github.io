## Jigsaw Puzzle Problem

Lately, I've been playing a lot of jigsaw puzzles on my phone.  One day, I noticed that when I started assembling the puzzle, focusing on the edges, I usually see two matching pieces next to each other.  What are the odds? I marveled.
And so, I obviously needed to calculate that.
First, I ran a simple simulation, to check some experimental results.  My favourite difficulty level of puzzle is a 15 by 15 puzzle which contains 225 pieces, of which 58 are edge pieces (feel free to count!).  I started by asking:
If I reorder the numbers between 1 and n, what is the probability that my sequence contains at least one consecutive pair?  (Here $n$ = 58)
I ran this with different $n$ values, and discovered that once $n$ got big enough (say 10 or more), it seemed to always give and answer between 85% and 90%.  Interesting.  But it must depend on $n$, yes?

For the sake of ease, I decided to not worry about the fact that my edges actually form a chain â that is, piece 1 is next to piece 2.  I'll correct that at the end.  [Note to Amy: Correct].

First,
Note:
* There are $n!$ possible orderings of $n$ objects.
* There are $n$ consecutive pairs [note n-1 if 1 isn't next to n]
* There are nC2 (n choose 2) possible pairs,

So:
$$Number of possible pairs = \frac{n!}{2(n-2)!}= \frac{n(n-1)}{2}$$
So, if I choose 2 pieces at random, the odds of them being consecutive are:
$$P(match)= \frac{#  Consecutive pairs}{total possible pairs} = \frac{n}{\frac{n(n-1)}{2}} = \frac{2}{n-1}$$

Now, back to the puzzle:
We are working in a binomial distribution with:
$n-1$ as the number of trials (that is, the number of possible pairs in my sequence)
$\pi= \frac{2}{n-1}$ is the probability of success:
And I am looking for P(X \geq 0) = 1- P(X =0):

So:
\[1-(n-1)C0 \times \frac{2}{n-1}^0 \left(1-\frac{2}{n-1}\right)^{n-1}\]
\[ =  \left(1-\frac{2}{n-1}\right)^{n-1}\]
For n = 58, we have:
\[P = 1- \left(1-\frac{2}{57}\right)^{57} = check\]
But what if $n$ is big?
Now we have
\[lim_{n \rightarrow \infty} = 1- \left(1-\frac{2}{n-1}\right)^{n-1} = 1-e^{-2}\]

Around 87%.






Part 2:  The whole puzzle
