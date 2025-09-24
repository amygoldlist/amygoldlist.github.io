---
layout: post
title: Roots of Polynomials with a Business Calculator

---
Twenty years ago, in the fall of 2005, I taught my very first Calculus class. It was a basic Calculus for Science class, and I spent that semester thinking about, talking about, and learning about how to effectively teach.  

I've done a lot of different things since then, but here I am, still teaching Calculus (though now mostly to Business students).

So in honour of my 20th anniversary of Calculus teacher, I present a (partial) solution to a problem one of my students brought to me:

## If all I have is a BAII Plus calculator, how can I find the roots of a quadratic?

In case you didn't know, Business school students typically buy a calculator for their Buiness Math and Financee classes, which has TVM (Time Value Money) built in.  This lets them calculate annuities very quickly and precisely, but often lacks some of the features that Scientific Calculators have.  My students use the Texas Instrumets BAII Plus calculator. 

<h5 align="center">
  <br>
<img src="/images/calculator.jpg" alt = "image" width="300">
<imgcaption>This is the basic BAII Plus, not the Pro. </imgcaption>
<br>
</h5>

The short answer should be obvious to my loyal readers:  Factor the quadratic!  Or use the quadratic formula:

If $ax^2+bx+c = 0$ than:

$$x = \frac{-b\pm \sqrt{b^2-4ac}}{2a}$$

## Ok, but I didn't memorize the quadratic equation. 

As it turns out, the answer is "we can find one root".  For this, I spent some time googling, and didn't find a good answer.  Next I went through the worksheets on my calculator, and found a partial solution.

The Cash Flow worksheet (CF) is used to calculate the NPV (Net Present Value) and the IRR (Internal Rate of Return).  It's the IRR I'm going to use.

If you set up a single Cash Flow in each year, so each one occuring with frequency 1, we have a Cash Flow Situation that looks like:

| Time    | Cash Flow     |
| ------------- | ------------- |
| 0| CF0 |
| 1 | C01|
| 2 | C02|

We're going to start with just two years of Cash Flow.  The IRR is given as a solution to the following equation:

$$ CF0 + \frac{C01}{(1+i)}+\frac{C02}{(1+i)^2}=0$$

To be consistent with the calculator, 

$$I = i\times 100$$
 
 as it is given in percent.
 
 ## Yes, but that's not a polynomial!
 
 Isn't it?  We need to remember that $1+i \neq 0$, but let's just multiply this through by $(1+i)^2$ on both sides:
 
$$CF0(1+i)^2 + \frac{C01(1+i)^2}{(1+i)}+\frac{C02(1+i)^2}{(1+i)^2}=0\times (1+i)^2$$

$$CF0(1+i)^2 + C01(1+i)+C02=0\times (1+i)^2$$

Now that's a polynomial! Especially if I let $x = 1+i$, and make sure $x\neq 0$.  

## What if it's a quintic?  or degree 17?
The beauty is that this method should work for any degree polynomial.  I'm going to work an example:


$$x^5-3x^4+x^3-5x^2+x -17=0$$


This has one real solution, at $x\approx 3.2788$, verified with Wolfram Alpha

My method means putting these numbers in the calculator:

| Time    | Cash Flow     |Frequency|
| ------------- | ------------- |-----|
| 0| 1 |-|
| 1 | -3|1|
| 2 | 1|1|
| 3 | -5|1|
| 4 | 1|1|
| 5 | -17|1|

Thes are the coefficients of our very fancy quintic equation.  When I put this into my calculator, I get:  $IRR = 227.88$.  Using the definition, we know that:

$$i = \frac{IRR}{100} =\frac{227.88}{100}= 2.2788$$ 

and

$$x =1+i = 3.2788$$

Which is what I said.

#### Explanation

The IRR should solve the equation: 

$$ 1 + \frac{-3}{(1+i)}+\frac{1}{(1+i)^2}+\frac{-5}{(1+i)^3}+\frac{1}{(1+i)^4}+ \frac{-17}{(1+i)^5}=0$$

By multiplying both sides by $(1+i)^5$, this is equivalent to:

$$1(1+i)^5-3(1=i)^4+1(1+i)^3-5(1+i)^2+1(1+i)^1-17=0$$

If we set $x = 1+i$, we have our original equation.


## What if there are multiple roots?

Now that's the problem! The IRR button uses approximation methods to find a single root: I'm not going to look this up or verify it in any way, but I like to think that it uses Newton's method to find the smallest positive root - that is, the answer most liekly to be an Interest rate.  

However, if we're solving calculus equations, we often care about all the roots.  In a business context, this is often the most important one!  However, we do need all of the roots, and this method does not work completely. 


## Proof by specific incorrect example:

Let's use this method on the easily solved equation:

$$(x-3)(x-5)= x^2-8x+15=0$$

Using our knowledge of factoring, we can see that the two roots are $3$ and $5$.  Plugging into our CF worksheet gives:

| Time    | Cash Flow     |Frequency|
| ------------- | ------------- |-----|
| 0| 1 |-|
| 1 | -8|1|
| 2 | 15|1|

and an answer of: $IRR = 200$ or from our earlier work: 

$$x = \frac{IRR}{100}+1 = \frac{200}{100}+1 = 3$$

But we know that 5 is also an answer!  We will still need to use algebra.



## But why do this, if it doesn't give a complete answer?

Great point!  I wouldn't.  Especially because finding the roots of a polynomial is a problem that can be approximated quite well by a computer.  On an exam, the quadratic equation is still the most useful method.  I wouldn't ask anyone to find the roots of a quintic (degree 5) polynomial on a test with just a business calculator, that would be mean!

However, constraints make for interesting solutions!  In Calculus this is definitely true, constrained optimization can be much more complicated and interesting than its unconstrained cousin.  It's also practical - we don't have unlimited resources, so maximizing with the resources that we have is a better business problem.  I think this applies in other ways as well - the first season of "White Lotus" was filmed during Covid, and the constraints of limited cast and crew, often outdoors made for a great season of TV.  Van Gogh didn't have the funds to buy every shade of paint, so he mostly worked in a limited colour palette


<h5 align="center">
  <br>
<img src="/images/poet_garden.jpg" alt = "Van Gogh" width="300">
<imgcaption>"Poet's Garden" by Van Gogh.  Image from the Art Institute of Chicago </imgcaption>
<br>
</h5>
 
 I'm not looking this up, but I was always told Van Gogh didn't have any green paint!  amazing.
 
The point I'm trying to make is that even if this method isn't useful, the act of thinking it through and working with an insufficient tool made me think more about the concept of Internal Rate of Return, and how my calculator worked.  I love doing this - that's why I've paistakingly recreated all the Statistics functions into [Excel worksheets](https://github.com/amygoldlist/Excel_fun).  This isn't even the first time I did something wacky with the BAII Plus Calculator - that would be [Learning Curves](https://pressbooks.bccampus.ca/businessmathematics/chapter/appendix-a-learning-curves-in-the-baii-plus/).  I highly encourage you to come up with an out of the box solution, even if it turns out to be not super useful.


## Conclusion, or back to that first Calculus class in 2005....

I've learned a lot about teaching over the past 20 years, but I think the lessons that I learned teaching MATH 180 way back when still hold:
* Just because I explain something really well, doesn't mean the students understand it.
* Listening to a a lecturer talk about Calculus doesn't actually teach.  It's the homework / labs / active work that actually gets the concepts in your head.
* The best resourse in learning how to teach is other teachers - Way back when, several of us new instructors / grad students made a teaching group where we talked things through and traded ideas.  I still count that group as some of my closest friends.
* It took me a lot longer to learn to talk with the students, and using their feedback to change my approach.  I wish I could say I learned that 20 years ago, but it took a bit longer.

## Updates
* I am working on a post about GenAI, which is taking longer than it should.  The upshot is it's a tool, it can't do everything, but it can do some things...
* My time as Program Head of the Business Analytics program has finally come to an end after almost 6 years.  However, I now am Program Head for AI Management, so I'm still doing more administration than needed.  I'm also serving as faculty rep on BCIT's Education Council, which has been a really eye openeing experience.  Also, all theRobert's Rules of Order I memorized in High School for model UN have really come in handy!
* I took an actual vacation where I did not do work for 6 weeks, which was....  so nice.
* Since Atom shut down, I'm looking for a new Markdown Editor, so feel free to send me recomendations.  
* This website could use a refresh, and I should probably add an RSS feed to the blog...
