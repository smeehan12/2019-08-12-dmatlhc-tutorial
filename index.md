---
layout: lesson
root: .  # Is the only page that doesn't follow the pattern /:path/index.html
permalink: index.html  # Is the only page that doesn't follow the pattern /:path/index.html
---

<figure>
  <img src="../fig/handson.jpg" alt="HandsOn" width="700" height="400">
</figure>

Welcome to the hands-on tutorial of the [DM@LHC conference at 2019](https://indico.cern.ch/event/783977/).
This tutorial should be viewed not as a comprehensive overview, as some of the talks later in the week,
but rather as a chance to get down into the nitty gritty of some of the tools that we use
in HEP, and at the LHC in particular, to study dark matter signatures.  Throughout the tutorial
you will learn about the following tools :
- [Docker](https://www.docker.com/) : For bundling and using software that would otherwise be a pain to install on your computer.
- [MadGraph](https://cp3.irmp.ucl.ac.be/projects/madgraph/) : For generating matrix element events from a myriad of BSM models.
- [Pythia](http://home.thep.lu.se/~torbjorn/pythia81html/Welcome.html) : To bring a matrix element parton-level event to the final stable hadron-level event.
- [Rivet](https://rivet.hepforge.org/) : For capturing a truth-level analysis.
- [Contur](https://contur.hepforge.org/) : For deriving constraints for a given model based on unfolded measurements.

> ## Prerequisites : i.e. [Docker](https://www.docker.com/)
>
> The absolute most important thing for this tutorial is for you to install [Docker](https://www.docker.com/).
> How you do this is covered in the **Setup** section below.  Please take some time to do this in the next days.
> It will greatly facilitate you making the most of the time we have at the workshop tutorial.
>
{: .prereq}

{% include links.md %}
