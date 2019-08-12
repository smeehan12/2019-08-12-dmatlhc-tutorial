---
title: "Rivet+Contur"
teaching: 20
exercises: 0
questions:
- "What is Rivet? What is Contur?"
- "What is an unfolded distribution?"
- "What do existing measurements say about DM signatures?"
objectives:
- "Execute an existing Rivet analysis pertinent to our monojet signature."
- "Transform the analyzed spectra into exclusion limits on the DMsimp model using Contur."
keypoints:
- "Rivet is a platform by which we can 'safely' analyze particle physics truth record data."
- "An unfolded spectra is one for which the effects of detector resolution have been removed through a deconvolution."
- "We can infer things about parameters in a model by using the CLs test statistic."
---

Now that we have a conceptual understanding of how we can go from a measurement to a meaningful
physics statement by using the power of likelihoods, let's contextualize this with the CONTUR tool.
CONTUR ([https://contur.hepforge.org/](https://contur.hepforge.org/), [1606.05296](https://arxiv.org/abs/1606.05296)) stands for **C**onstraints **O**n **N**ew **T**heories **U**sing **R**ivet
and aims at making as broad use of the wealth of measurements from the LHC, and really any other collider
experiment for that matter, by using the Rivet ([https://rivet.hepforge.org/](https://rivet.hepforge.org/))
analysis preservation paradigm.  In its current incarnation, doing so requires that certain approximations
are made which limit its power as compared to dedicated searches and it is further limited to only
those final states that are available as preserved [Rivet routines](https://rivet.hepforge.org/analyses/).  However,
as you will (hopefully) see, even with these limitation it can serve to be incredibly powerful in providing
broad constraints and help guide us to see which

## Truth Analysis

## Unfolded Spectra

## Running Rivet

## Running Contur



{% include links.md %}

