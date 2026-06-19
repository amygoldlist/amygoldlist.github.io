---
layout: post
title: Triangles
mathjax: true
---
 <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
 
What is a proof?

Since this is my blog, and I get to talk about anything I want, let's talk about numbers.  People who know me know that I love technology, data, teaching and al the things I do in my work life.  But you probably also know that I started my academic career as a mathematician, and matheticians never stop thinking about the world that way.

I've got a student in the first stages of proofs, and talking about proofs is delightful.  So I give you some of the questions that we have been working on.  I will keep on saying it - I learn a lot from my students.  (Especially this year's crop of AI Manangement students, graduating next week.  You guys know who you are, and I've learned more about AI prompting from your documentation than from anny course)

## Where do problems come fom?

They come from anywhere!  Numbers are all around us, and if you stop to think about them, you will find more questions than answers.  During my boring tasks like exercising or folding laundry, I often think about how much time I have left.  "I'm walking 8 blocks total, I've gone 2 blocks, that's a quarter".  Once I've got a fraction, I try to break it into Egyption fractions - a sum of fractions with 1 as a numerator.  

This can look like "I'm 8 minutes into a 30 minute exercise session, that's...."

$$\frac{8}{30} = \frac{4}{15}= \frac{3}{15}+\frac{1}{15}=\frac{1}{5}+\frac{1}{15}$$

That's very satisfying, and by the time I've got it worked out in my head, I'm probably now$\frac{9}{30}= \frac{1}{5}+\frac{1}{10}$ of the way through my task.

I'm not going to tell you all about Egyptian fractions, but I will thank my Grade 9 math teacher, Mr. L., for letting me sit at the table at the back of the room with a book about Egyptian mathematics, instead of regular fractions.  I will say, one can ask a lot of questions:

* Is every rational number expressible as Egyptian Fractions?
* What is the minimum number of terms in an Egyptian Fraction?  
* Is there an Algorithm to find it?

Look it up if you're interested!  


## I thought you said triangles?

When I'm stressed and need to relax, I can't sit and watch television or talk without doing something with my hands.  For this, I knit.  I'm a good knitter, and I can make all sorts of sweaters, hats, stranged colour work, cables, stuffed animals.  But what I like best is a simple dishcloth.


<h5 align="center">
  <br>
<img src="/images/knit.jpg" alt = "stack of dishcloths" width="300">
<imgcaption>It's my dishcloths! </imgcaption>
<br>
</h5>
 
For the pattern I knit, you cast on, and increase once every row until you have a nice diagonal length, then you decrease once per row until your done.  Easy!  But sometimes, I just want to know:

>Am I half done my increases?

Great question Amy!

## Triangular numbers

If the first row has one stitch, ad we increase every row, the $n$th row has $n$ stitches.  And when I'm finished the $n$th row, I have a total of:

$$\Sigma_{i=1}^{n}i = \frac{n(n+1)}{2}$$ 
stitches.

That's what we call a triangluar number.  I'm not going to explain where this equation comes from, but I encourage you to think about it and try on your own. My student proved this by induction, and I couldn't be more proud.

That means that if I want 40 rows (which I always do, it just really is the best width), I need:


$$\Sigma_{i=1}^{40}i = \frac{40(41)}{2}= 820$$
stitches in total before I can start my decreases.  Half of this is 410.  Can I backsolve, to find out how many rows that would take?  It's not 20 rows, at 20, I've only done 210 stitches!



<h5 align="center">
  <br>
<img src="/images/triangle_board.jpg" alt = "my whiteboard" width="300">
<imgcaption>A formula.  Of sorts</imgcaption>
<br>
</h5>

I am leaving this as an exercise for the reader to generalize, but I'll let you know that my formula says I'm halfway to the decreases a few stitches into row 28.


## Ok, but you didn't actually give me the general formula!  What is it?

It's there, it was on my board, and on the sheets attached, and that's good enough for me.  This post isn't about answering questions, it's about thinking like mathematician.  Look around the world, and come up with good questions.  That's the most important!


## Pattern
This pattern came from a ball of Bernat Handicrafter yarn, a long time ago.  I modified it!  

>Cast on 2 stitches
>
>K1, Kfb
>
>K, Kfb to end of row
>
>Repeat until there are 40 stitches
>
>K2, K2tog, K to end of row
>
>Repeat until there are 4 stitches left, 
>
>Cast off, weave in ends.
>
>Clean your dishes!


