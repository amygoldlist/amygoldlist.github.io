---
layout: post
title: Quiz questions in D2L Brightspace part 2, R/exams
---

*This Project lives [on Github](https://github.com/amygoldlist/D2L_exams)*

In the last post, I introduced the concept of creating algorithmic questions in D2L Brightspace. Recall: 2L Brightspace (At BCIT we call it the Learning Hub) makes giving online tests run very smoothly. However, their numeric question types are limited to basic arithmetic, and only have single answer (not multi-part) questions.

Our Business Math group over at BCIT is working on making math exams work better for us - dynamic and algorithmic questions dealing with Statistics, as well as multiple choice questions that can be different for each student.

This post is going to concentrate on creating dynamic multiple choice questions using r.  If you are interested in other methods, check out my [previous post](https://amygoldlist.github.io/2021-01-15-Exams-in-D2L/) which concentrated on using Respondus and Excel.

### Method: R-exams:  

[R/exams](http://www.r-exams.org/),  makes creating dynamic exams much more fun.  Since there doesn't seem to be a lot of information online about how to use this for [D2L Brightspace](https://www.d2l.com), I've put some of my work on Github.  There is no  `exams2d2l()` command, but luckily, the command `exams2blackboard()` creates a file that imports properly into D2L.  This makes sense, as both blackboard and D2L are based on the same QTI1.2 format.

If you're interested in this topic, please download the source files for this example.

The following questions were part of a Statistics test, and the questions themselves were crafted by my colleagues Judy Li and Germain Tanoh.

There are two main ways to craft Multiple Choice Questions in R-exams:

#### Numeric Answers
*follow along with this [question](https://github.com/amygoldlist/D2L_exams/blob/main/D2L_exams_demo/exercises/J09_france_mc.Rmd)*

I started with a question

>Rendezvous en France has found that 60% of vacationers visit Paris, 25% visit Marseilles and 20% visit both Paris and Marseilles.   What percentage of vacationers to France visits at least one of the cities?
>
>(a)	85%	   60%+25%\
>(b)	35%	   find P(neither)\
>(c)	65%    correct answer\
>(d)	70%  	 minus 0.6*.25\
>(e)	80%	   60%+20%

Helpfully, I was provided with algorithms to generate the incorrect answers, which is extremely important.

We start by creating an R-markdown file, and deleting the preamble.  All of hte code for the question can be in a code chunk:

In order to make this question more difficult to google, I randomly generated two French cities, which would vary.  Changing the name of the publication would also help.

```
## To begin, let's vary the two cities, to make this question harder to google.
cities <- c("Paris", "Marseilles", "Dijon", "Avignon", "Nice", "Lyon", "Toulouse", "Nantes", "Montpellier", "Bordeaux", "Strasbourg", "Lille", "Aix-en-Provence", "Metz", "Limoges", "Calais", "Pau")

## This samples two different cities, city[1] and city[2]
city <- sample(cities, 2)
```
Next we can generate some probabilities.  I don't get super fancy, all that I do is sample numbers:

```
## Now, generate the intersection of the cities:
P_both <- sample(10:20,1)
P1_not_2 <- sample(30:50,1)
P2_not_1 <- sample(10:25,1)

## and find the probability for each event.
P1 <- P_both+P1_not_2
P2 <- P_both+P2_not_1


## I always create the code for the correct answer:
ANS = P1+P2_not_1
```

When everything in sight is numeric, we can use the function `num_to_schoice()` to create the list of possibilities.  The advantage to this is that the algorithm can make sure that your distractors aren't to close to each other, or the real answer.  

```
## single-choice list
## Important:  you need to use this function to create the list of possibilities
## delta = minimal distance between solutions
sc <- num_to_schoice(ANS,
                     wrong = c(100-ANS,
                                    P1-P2,
                                    P1+P2,
                                    P1+P_both,
                                    P2+P_both), delta = 0.1, digits =0)

```
The question itself lives in a non-code chunk of the Rmd file - again, please look at the file!  Any variable lives in: \`r variable\`

> Question\
\==============\
Rendezvous en France has found that \`r P1\`% of vacationers visit \`r city[1]\`, \`r P2\`% visit \`r city[2]\` and \`r P_both\`% visit both \`r city[1]\` and \`r city[2]\`.   What percentage of vacationers to France visits at least one of the cities?

Now we use the object `sc` that we already created to display the answer list.  I've added code so that a percent sign will display at the end of each answer.  This lives in its own code-chunk, under the question.

```
## here are my possible answers, displayed as %
answerlist(paste0(sc$questions,"%"), markup = "markdown")
```
Finally, include the meta-information.  We could have created more than 4 wrong answers, and in that case, the algorithm would randomly pick 4 incorrect and the correct answer, and shuffles them.

```
Meta-information
================
extype: schoice ## Single Choice
exsolution: `r mchoice2string(sc$solutions)` ## finds the correct answer
exname: J09_france_mc  ## the name
exshuffle: 5  ## display 5 answers
```

Importantly, to generate this, we need another file, this one a script, that will call this question.  You can see this [here](https://github.com/amygoldlist/D2L_exams/blob/main/D2L_exams_demo/Demo_exam_master_script.R):

```
## load any packages we need:
library("exams")
library("tth")
library("base64enc")
library("dplyr")
library("scales")


### check the questions individually.
### This is useful for trouble shooting, but we are only viewing in html,
### not on D2L, so it's not perfect.
exams2html("Exercises/J09_france_mc.Rmd")

## list all the questions:
myexam -> "Exercises/J09_france_mc.Rmd"

## create the exam:

exams2blackboard(myexam,
                 name = paste0("Stats_test", Sys.Date()),
                 n = 15,  ### how many copies of each?
                               zip = FALSE)

```

(My computer has issues with zipping, so I manually do this.)  This generates a file that you can zip, and upload into D2L.

### Method:  Creating your own distractor Answers
*follow along with this [question](https://github.com/amygoldlist/D2L_exams/blob/main/D2L_exams_demo/exercises/J06_mode_mc.Rmd)*

Sometimes you want words to appear in your distractors, or you just don't want to mess with the `num_to_schoice()` function.

We start with a different question:

>	A teacher wishes to use the mode to measure the performance of his Business Statistics class. Below are the final exam grades for 10 students:
>
>53      75     53        78       95      75       92         75          20      95  
>
>Based upon this information, what is the class mode? (A)\
>A. 75\
>B. 53\
>C. (53, 75, 95)\
>D. No mode\
>E. 95\

This question was carefully generated so there was a single mode, with 3 occurrences, and two other numbers that have two occurrences.  The generating code block was simpler:

```

library(dplyr)

### generate a data set with 10 items, 3 of 1, 2 of 2 others

## create a list of 6 distinct numbers
d1 <- sample(45:95,6, replace = FALSE)
##create a 2nd copy of 3 of them
d2 <- sample(d1, 3, replace = FALSE)
## add a third copy of just one of the numbers and shuffle them all.
dat <- c(d1,d2,d2[1]) %>% sample(10, replace = FALSE)

```
There are no other code blocks, the rest of the question looks like:

>Question\
> \==============\
> A teacher wishes to use the mode to measure the performance of his Business Statistics class. Below are the final exam grades for 10 students:
>
>\`r dat\`
>
>Based upon this information, what is the class mode?
>
>Answerlist\
>\----------
>\* \`r d2[1]\`\
>\* \`r d2[2]\`\
>\* \`r d2[3]\`\
>\* (\`r sort(d2)\`)\
>\* No Mode
>
>Solution
>\========
>
>\`r d2[1]\`
>
>Meta-information
>\================\
>extype: schoice\
>exsolution: 10000\
>exname: j06_mode_mc\
>exshuffle: 5


Here the answer 10000 showing that the first answer is true, and the rest are false.

Multiple Choice questions are useful for quick, simple questions.  If you have questions, please drop me a line at Amy_Goldlist@BCIT.ca.
