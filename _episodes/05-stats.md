---
title: "LHC Statistics"
teaching: 20
exercises: 0
questions:
- "How do we make meaningful and robust statements "
- "What is "the profile likelihood fit with CLs test statistic"?"
- "How do we draw an exclusion boundary?""
objectives:
- "Review the basic concept of statistical likelhoods.""
- "Appreciate the power of 'toy monte carlo'."
- "Understand how limits are derived after making an observation of an event yield."
keypoints:
- "Likelihoods connect observations with parameters by giving us a sense of "how likely a particular dataset was given a set of parameters"."
---

**DISCLAIMER** : The use of statistics in HEP is pervasive and always constitutes the final
step in a search to make an "interesting" physics statement.  Many tools (e.g. [RooStats](), [HistFactory](), [pyhf]())
have been developed that can largely let you plug in your data and get out a number.  Doing so is dangerous
and you should always be encouraged to understand what they are _actually_ doing.  However, this
can be challenging and requires digging into a bit of statistics that may not be super intuitive.  Presented here
is a very brief story that is meant to give you a basic appreciation.  However, for the full story, you
should sit down with a few coffees and read [1007.1727](https://arxiv.org/abs/1007.1727), which can also
be found in slide format here (K. Cranmer [[1]](https://indico.cern.ch/event/117033/contributions/1327652/attachments/55755/80228/Cranmer_L1.pdf) [[2]](https://indico.cern.ch/event/117033/contributions/1327629/attachments/55733/80186/Cranmer_L2.pdf) [[3]](https://indico.cern.ch/event/117033/contributions/1327622/attachments/55727/80175/Cranmer_L3.pdf)).

## Likelihoods : The Distillery of HEP

The observations that we make are on the total yield of the number of events in our signal region.
After doing a search properly, this observation will be accompanied by a robust estimation of
the expected yield of background events as well as the purported yield of signal for the
model you want to test.  These observations and predictions may further be divided into a number of
"bins" if the search is done differentially as a function of some special observable (e.g. MET)
but fundamentally this is no different than having a sequence of signal regions.  Now, what we
want to do with this set of {observation, background, signal} is determine if the observations
look more like they were produced in a universe where **only** background processes exist ("B"), or
in a universe where both background and signal processes exist ("S+B").

FIG : one spectrum

To do this, we need get a bulk sense of what background only experimental results "usually" look like
as opposed to signal+background results "usually" look like.  Now let's pretend(*) we have divine control over the
universe in addition to a lot of money and can perform a run of the LHC over and over again after flipping
some super powerful switch to toggle whether the LHC collisions you produce are B or S+B.  This would allow
you to repeat the same experiment (i.e. ATLAS/CMS/LHCb Run 2 140ifb dataset) many times and build an intuition
about what that set of observations would look like in the two scenarios.

FIG (top): Series of B-only repeats

FIG (bottom): Series of S+B repeats

Great, sort of.  This is a lot of information and with so many bins, it is multidimensional.  It makes my head hurt
and is challenging for us to build an intuition about "what it looks like", so the next thing we will do
is distill the observations and predictions, along with perhaps all of the bins for a given experiment if it
really is a differential spectrum and we want to consider all of them at once, into a single number.  This number
is what we will call the **test statistic** and is itself a **likelihood** function.  It can be any function which transforms all of the information we
have at our disposal to a single number, but there are some good choices and some bad choices, like always.


EQN Top : CONCEPTUAL distillation

EQN Bottom : Example from Contur

Moreover, at the LHC, after choosing this initial function it is standard practice to make things "a bit more complicated"
by wrapping up in one package the evaluation of this function twice and taking the ratio of the two outcomes as below; we
now have a ratio of two likelihoods ... but this is just another likelhood; its a function.

EQN : Likelihood ratio with hats.

This is typically where people get a bit caught up but brings us to one of the main buzzwords : **"profile likelihood"**.  There are a number of hats
in this equation and to a statistician a hat represents the idea that the parameter under the hat is set to the value
which itself [maximizes the value of the likelihood function](https://towardsdatascience.com/a-gentle-introduction-to-maximum-likelihood-estimation-9fbff27ea12f).
But there are parameters for which there is one hat and some that have two.  That is because we take this one step further
and single out a single parameter which is the signal strength ("mu") which is the main parameter of interest and scales the
normalization of the amount of signal and is referred to as the "signal strength". Then, the one hat in the denominator refers to
allowing all parameters to float and find their overall "best fit" values for the denominator likelihood function.
However, in the numerator where we have two hats, what is happening is that we are toggling the signal strength to be
precisely the value of "mu" and nothing else and finding the values of all the other parameters that maximize the numerator likelihood.
After performing these two values and taking the ratio of likelihoods, we have our final single number _for that single example experiment_.
Moreover, it was calculated for only one of the choices of B-only (which is nothing more than setting mu=0) or for some specific
value of mu. This entire procedure
is what we mean when we say "profile likelihood ratio test statistic".  The final *test statistic* is composed of a *ratio* of two *likelihoods*,
both of which have been **profiled**, which refers to the procedure of maximizing the parameters as described above.   [Warning : If this is your first time seeing this, go back and read this paragraph again.  Once you understand it, like really
internalize it, you can count yourself to be a part of an elite group of too few particle physicists who know what this buzz-phrase actually means.]

FIG Distilling of distributions

We can then use our immense divine powers to do this hundred of times and make a distribution
, which is now only in one dimension, for both of the cases we care about {B-only : mu=0 , S+B : mu=s}.
That's great, now we have a much more simplified intuition for "what a B-only experiment looks like".
That is, if we toggle the switch and produce another set of B-only data and distill it through our
profile likelihood ratio test statistic, we will probably find a value close to the mean value of the previously generated ensemble.
We can then do the same thing, but using our real data, which itself will produce only a single value of the test statistic.
However, this time we are armed with our understanding of what B-only or S+B look like and we can use that to make
a meaningful statement about the experiment we actually did produce

FIG : distributions with the real data test statistic on top and posing question

> ## Neyman Pearson Lemma
>
>
>
>
{: .callout}

> ## Toy Monte Carlo : Make Believe
>
>
>
>
>
{: .callout}

> ## The Asymptotic Approximation
>
>
>
>
{: .callout}

(*) We are only going to "pretend" of course because if we had divine control, we would probably
also know whether our data has signal in it in this universe, but bear with me.


## Discovery





## Exclusion




> ## Origins of CLs
>
>
>
>
{: .callout}


## Mapping out the Space : "Contouring"
