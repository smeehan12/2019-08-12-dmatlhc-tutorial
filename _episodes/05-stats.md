---
title: "LHC Statistics"
teaching: 20
exercises: 0
questions:
- "How do we make meaningful and robust statements "
- "What is "the profile likelihood fit with CLs test statistic"?"
- "How do we draw an exclusion boundary?"
objectives:
- "Review the basic concept of statistical likelhoods."
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
as opposed to signal+background results "usually" look like.  Now let's pretend(\*) we have divine control over the
universe in addition to a lot of money and can perform a run of the LHC over and over again after flipping
some super powerful switch to toggle whether the LHC collisions you produce are B or S+B.  This would allow
you to repeat the same experiment (i.e. ATLAS/CMS/LHCb Run 2 140ifb dataset) many times and build an intuition
about what that set of observations would look like in the two scenarios.  We call each of these
repetitions of the experiment a **pseudo-experiment**.

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

(*) We are only going to "pretend" of course because if we had divine control, we would probably
also know whether our data has signal in it in this universe, but bear with me.


## Discovery

To work towards understanding how we can use this likelihood to make a meaningful statement, let's
start with **discovery**.  Although this is not the case that we will eventually be interested
in understanding for CONTUR, we can begin to get a sense of the core concept of a p-value and a
confidence level (CL).

Here, we will use the distribution of the B-only likelihood to benchmark how compatible our data
were with it.  It peaks at low values and so if we evaluate the test statistic for our single dataset
and it takes on a large value, then perhaps we feel a bit suspicious.  However, you should
diligently recognize that there is a long tail in the distribution of the B-only likelihood
so there are some cases (because of statistical fluctuation) that we toggled our divine switch to a
B-only universe, but it generated an anomalously high value for our test statistic.  So instead,
let's quantify how "strange" this one experiment is by evaluating the fraction of pseudo-experiments
in our toy generation that had a resulting test statistic that was larger than the experiment in question.

FIG : p-value one sided

This value, the fraction of "more discrepant pseudo-experiments" is what we refer to as the **p-value**
for the one experiment in question.  The lower it is, the more suspicious we become.  And if
it is so friggin' small that it feels "impossible that a B-only experiment could have produced
an experimental outcome that looks like that", then it means we have a discovery.  The real statement
we are making at this point actually only pertains to the consistency of the data with the B-only hypothesis
and doesn't necessarily mean that we have discovered a new particle, but could instead mean that
our background estimate is rubbish.

This p-value is also referred to as the **Confidence Level (CL)** for the interval defined from the value
of the test statistic calculated for the data and infinity.  And because it is calculated with respect to the
B-only hypothesis is appropriately called "CL(b)".

> ## 5 Sigma
>
>
>
>
{: .callout}



## Exclusion Limits

Now that we have the notion of a CL value (or a p-value) for an interval, let's set a limit.  If we are
setting limits, then it means to a large extent that we have already evaluated CL(b) and found it to be
unexciting.  Therefore, we know that the test statistic for the data lies somewhere near the bulk
of the B-only likelihood.  And now, since we want to make a statement about the interesting physics
parameter of the signal strength, then we are going to begin by leveraging the S+B likelihood, and
study its behavior with respect to the value of the test statistic calculated for the single real
experiment.  In particular, we are going to calculate the value of CL(s+b) which is the p-value
of the one-sided confidence interval that tells us "How much does the data actually look like it
was produced from the S+B hypothesis?".

FIG : likelihoods with the data shown and one CLS+B

Now, the example above is only considering one specific choice of the amount of signal that we are
testing, it is only one specific signal strength.  Moreover, it is only one specific choice for
the entire ensemble of interesting physical input parameters in our model (e.g. particle masses and
couplings).  Therefore, to determine what **region of parameter space** is excluded for this set of parameters, we can fix
them and create multiple S+B likelihood spectra for an ensemble of signal strengths {s0, s1, s2, ... sn}.  Yep,
this means we will actually no longer be using our divine _switch_ but rather our _divine throttle_ and for each
individual setting, we will be recreating the LHC dataset and ATLAS/CMS/LHCb experiments many times to generate
the distribution of CL(s+b) values for that particular choice of s.
For each of these, we can calculate the value of CL(s+b).  Since the data has already been determined to look
quite like the background (i.e. it has a rather large CL(b) value) then we can examine the CL(s+b) value
and if for some value of si, if CL(s+b) is smaller than some pre-established value then we conclude that "it
is obviously not possible that a signal with that cross section exists" and we **exclude** that signal strength
... and also all cross sections larger than it.

FIG : likelihoods with decreasing CL(s+b) values


> ## The Asymptotic Approximation
>
>
>
>
{: .callout}

From here there is only one final step to arrive at what is "actually" done at the LHC.  Throughout
this entire procedure, we have discussed only the CL(b) and CL(s+b) p-values.  However, at the LHC
a slightly different definition of a confidence level is used; the **CL(s) value**.  This is defined
as the _relative_ confidence level of the S+B hypothesis to the B-only hypothesis.  So, in reality
for each of the signal strengths {s0, s1, s2, ... sn}, we calculate the CL(s) value and when this drops below
a certain value, then we conclude that that signal strength (and all those above) are excluded.  The value
that we typically choose for this threshold is 2-sigma (which is a Z-value) and translates to 0.05 (which is a p-value).

EQUATION of CLS and the combined plot.

> ## Origins of CLs
>
>
>
>
{: .callout}

> ## Expected Limits
>
>
>
>
>
{: .callout}


## Mapping out the Space : "Contouring"

Going from the output of the "profile likelihood fit with CL(s) test statistic" machinery
covered above to a fancy exclusion contour that is the "interesting" physics output
of the search is rather straightforward from here, although the amount of computation
may be rather large.  Essentially, we simply have to determine the region of parameter
space in the model that we are interested in exploring, and to which we believe we may
be sensitive to.  We then generate a set of signal samples for an array of points in this parameter
space.  This is typically done in one of a few ways ""

- Generating : Rerunning MadGraph+Pythia for each unique set of parameter choices.  This is the brute force manner and most straight forward.
- Morphing : Running MadGraph+Pythia for a few choices of parameter settings and then *interpolating* between these points by parameterizing the signal and then tuning the empirical parameters.
- Reweighting : Similar to morphing, you can generate a few representative points and then determine a set of event-by-event weights that perform and effective interpolation between those points.

This will result in what is commonly referred to as a "signal grid".  For each of the points in this grid,
you can then perform the procedure outlined above which produces the cross section (_for that point_) which
is disallowed based on the observed data from the _actual_ running of the LHC (as opposed to your
divinely inspired pseudo-experiments). Finally, you compare the value of the cross section which is excluded to
the theoretically predicted cross section that MadGraph (or some method) tells you the theory would
generate if it exists.  If this predicted cross section is greater than the level of excluded cross
section then you can rule out that point in parameter space.  The final step is to examine your
signal grid and find the boundary that separates the points that were excluded from those which
you "failed to exclude".

FIG : signal grid, excluded points, contour over excluded points

And voila! There is our contour! Now let's venture on and see how we can use CONTUR to produce a contour.















