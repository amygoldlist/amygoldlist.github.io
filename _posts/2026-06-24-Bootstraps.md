---
layout: post
title: Repeated Bootstrap Sampling, or Why does AI always sound the same?
mathjax: true
---
 <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
 
 
 *This post is in development.  Also, as usual, I wrote everything myself, but Claude Code made the applets*
 
# Motivating Story

This is a wild time to be an AI teacher!  By the time I get to class, my lesson plan is out of date.  I try to teach a new tool, and a student will quielty send me corrections on best practices, because their AI agents are better than mine.  At some point, I started going with the flow and getting them to demonstrate their AI use as part of class  - I've learned way more by listening to them, then any webinar offered by an AI company.

One Friday, we worked on a group activity in lab.  The brief was to get into groups, and use any GenAI tool to create a short presentations on Reinforcement Learning.  My goal was to have them do the activity, assess their knowledge of the subject, and then assess them on it.  On Monday, we had a scheduled Old School leson scehduled to start our unit on Reinforcement Learning.  I was wondering if having AI create the presentation helped their learning, or not.

The activity did not go as planned.



<h5 align="center">
  <br>
<img src="/images/Bootstraps/claude_RL.jpg" alt = "Results from Claude" width="300">
<br>
</h5>


 By the third presentation, the students were murmuring.  By the fourth, they were laughing.  The presentations were all the same - despite having been run through different models, with different prompts.
 
 To demonstrate, I've run the same prompt through differnent models, 
 
 
 >Can you quickly explain exploration versus exploitation in Reinforcement learning?
 
 *All models were queried on June 24, 2026*
 
 ---

 ### [Claude Opus 4.8](https://claude.ai/chat/98171293-e040-4aed-8777-b83be198379f)
 
 *image above, here's the relevant paragraph:*
 
 
 >A classic way to picture it: imagine you've moved to a new town with several restaurants. You could keep going back to the one decent place you've already found (exploitation), guaranteeing a meal you know is good. Or you could try an unfamiliar restaurant (exploration), risking a bad dinner but possibly discovering somewhere much better. If you only ever exploit, you might never find the best restaurant in town. If you only ever explore, you waste a lot of meals on mediocre places and never settle into enjoying what you've found.
 
 ---
 
###  [ChatGPT, base free model](https://chatgpt.com/c/6a3c5673-ec20-83e8-9f88-3cf878bb70e3)
 

<h5 align="center">
  <br>
<img src="/images/Bootstraps/gpt_RL.jpg" alt = "Results from ChatGPT" 
<br>
</h5>


> Imagine choosing a restaurant for lunch:
>
>* **Exploitation:** Go to your favorite restaurant because you know it's good.
>* **Exploration:** Try a new restaurant that might be better.
>
>If you always exploit, you'll never discover hidden gems. If you always explore, you'll never consistently enjoy the restaurants you already know are great.

---

### [Gemini Flash](https://gemini.google.com/app/aecbe44a7834a3eb)


<h5 align="center">
  <br>
<img src="/images/Bootstraps/gemini_RL.jpg" alt = "Results from Gemini" 
<br>
</h5>


> **Exploration: Finding New Knowledge**
> * **Real-world analogy:** Trying a brand-new restaurant you've never been to. It could be the best meal of your life, or it could be terrible.
>
> **Exploitation: Using Known Knowledge**
> * **Real-world analogy:** Going to your favorite local diner and ordering your usual burger. You know exactly what you're getting, and you know you'll like it.



I've recreated the analogy that was in every presentation - Order what you know you love, or try something new.  (It's funny, because if you've ever been to a restaurant with me, you know what I'm going to order.  Same thing as last time!)   Below, I asked ChatGPT to come up with some LLM cliches: 


---
## "It's not a cliche—it's a fact."

>> At its core, success isn't about working harder—it's about working smarter. The key isn't perfection; it's consistency. While many people focus on short-term results, the reality is that lasting progress comes from small, deliberate actions over time. Ultimately, the question isn't whether you can achieve your goals—it's how you'll adapt when challenges arise.
>
>You can almost hear the token probabilities humming. 😄




It's been a few months, and I've been noticing this patern everywhere.  LLMs are probablistic models.  They create new and creative answers to queries, and the same question might get quite different results.... or do they?  If you are working with LLM output, you might also have noticed that they seem less creative than they once did.  Every student in my Machine Learning class independantly chose 42 for their random seed.  Teh same word constructs appear in mutiple papers.

I've got a hypothesis of what is going on.

## Bootstrap Sampling

Time to talk Stats!  When we sample from a population, we have two options: 
* Sample without replacement (like dealing a hand of cards.  You can only get one King of Hearts.)
* Sample with replacement (like rolling a die five times.  You might get two sixes.).  We sometimes call this "Bootstrap Sampling".

## Try it
_Claude Code created these lovely Applets._

<iframe src="/images/Bootstraps/sampling-wr.html"
        width="100%"
        height="700"
        style="border:none; border-radius:14px;"
        loading="lazy">
</iframe>

With this type of sampling, it's easy to make a sample that is larger than the original.  Play around with the numbers above!  That's why we often use this as a Sampling method when dealing with small samples.  If you've taken a Statistics class with me, you might have heard me warn against this - it's a powerful method, but there are some drawbacks to using this instead of conventional sampling.

## Repeated Bootstrap Resampling.

Take a sample, bootstrap from it.  Than bootstrap from your bootstrap.  Then do it again. And again.  I'm calling this bootstrap resampling.  I might update this with some lovely math, but my theory is that most of the time, this leads to a homogeneous population.  

Try sampling and resampling, over and over:

<iframe src="/images/Bootstraps/bootstrap-a.html"
        width="100%"
        height="700"
        style="border:none; border-radius:14px;"
        loading="lazy">
</iframe>


Play with different values, constantly resampling from the previous resample.  Most of the time, it will converge to a homogensous population - that is, alll the balls will look the same.  



<h5 align="center">
  <br>
<img src="/images/Bootstraps/five_by_five.jpg" alt = "An example" 
<br>
</h5>

In this case, we've started with a *hetereogeneous* population - a uniform distribution of coloured balls.  Eventually this converges to a row of all one colour.  Which colour?  It's impossible to tell at the begining, but with small enough balols, you can find out.

If we start with more balls, does it improve?

<h5 align="center">
  <br>
<img src="/images/Bootstraps/ten_by_five.jpg" alt = "Another example" 
<br>
</h5>

No, it does not!  We lose most of that information very quickly.  If we make a big resample, it will take longer, but it still loses some colours fairly quickly:

<h5 align="center">
  <br>
<img src="/images/Bootstraps/five_by_ten.jpg" alt = "Another example" 
<br>
</h5>

In this particular example, it took 11 rounds to end up with a row of purple balls.  However, you can see that by row 6, we only had two colours left. 


## OK, but why are LLMs boring?

> `random.seed = 42`
> 
> "It's not X -- it's Y."
> 
> "At a visit to a favourite restaurant, you have a dilemma: order the same great dish every time, or try something new that might end up being better?"

My hypothesis is that we are essentially in a large repeated Bootstrap experiment.  The early LLMs were trained on a vast amount of data - say all of the colours of the rainbow.  As we started using them to produce content, creating a large amount of output, this was added to the training data of later models.  Essentially, on a very large scale, we've been pulling balls out of the box, creating content, and feeding it back to the machine.  We've created a boring model, one that inevitably will choose `random.seed = 42` anytime you write Machine Learning code.  Was this inevitable?  No, I think it was inevitable that LLMs would become less creative, but these particular quirks of LLMs were just the luck of the draw.


### References:
*It's actually really tough to find out why LLMs say what they say!  So some of these are my best guess.*

* [https://claude.ai/chat/98171293-e040-4aed-8777-b83be198379f](https://claude.ai/chat/98171293-e040-4aed-8777-b83be198379f)
* [https://chatgpt.com/c/6a3c5673-ec20-83e8-9f88-3cf878bb70e3](https://chatgpt.com/c/6a3c5673-ec20-83e8-9f88-3cf878bb70e3)
* [https://gemini.google.com/app/aecbe44a7834a3eb](https://gemini.google.com/app/aecbe44a7834a3eb)
* My guess on why 42 is always the random number is that it is in some [`sklearn`](https://scikit-learn.org/stable/index.html) documentation, but probably from Douglas Adams classis "Hitchhikers Guide to the Galaxy"
* My best guess on the restaurant analogy is that it came from Richard Feynman.  Here's a recent Nature article explaining.  [https://www.nature.com/articles/d41586-026-00821-4](https://www.nature.com/articles/d41586-026-00821-4) Note:  you will need a Nature subscription.
