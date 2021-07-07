---
title: "MadGraph+Pythia"
teaching: 20
exercises: 3
questions:
- "How does a Monte Carlo simulation work?"
- "What is the difference between MadGraph and Pythia?"
- "What is the final output product of this simulation?"
objectives:
- "Configure a MadGraph BSM physics process simulation."
- "Calculate the cross section for a physics process."
- "Produce a HEPMC file for the monojet DM signature."
keypoints:
- "MadGraph simulates the matrix element physics process."
- "Pythia simulated the parton shower physics process."
- "MadGraph+Pythia allows you to produce a HEPMC file which contains information about the ensemble of stable particles that enter the detector."
---

## Starting Up
Start by pulling and booting up the docker image that contains everything you need for this tutorial
~~~bash
docker pull smeehan12/dmatlhc2019-tutorial:v0
docker run --rm -it -v $PWD:/contur/local smeehan12/dmatlhc2019-tutorial:v0 bash
~~~
Note that in this second command, there are a few optional arguments `--rm -it -v $PWD:/contur/local`
that come along with the `docker run` command.  Of these, of particular importance is the `-v $PWD:/contur/local`
argument which mounts (i.e. mirrors) the current directory where you are working on your local computer (`$PWD`)
to the directory called `/contur/local` within the image.

If things have worked correctly, then you can do an `ls` within the image and you should see
~~~
meehan:DMLHC2019 > docker run --rm -it -v $PWD:/contur/local smeehan12/dmatlhc2019-tutorial:v0 bash
[root@86371ca8f470 contur]$ ls
AnalysisTools   Makefile  README.md  contur.log     local              setupContur.sh
MG5_aMC_v2_6_6  Models    TheoryRaw  conturDemo.py  modified_analyses
~~~

Try creating a file in this local directory, and see if it appears on your local machine. **IT WON'T**!

However, if you instead create a file within the `local` directory within the image, then it **WILL** appear
in the directory where you booted the image on your local machine.  It will then persist on your local machine,
whereas all other content and files you create while you are working within the image will vanish when you exit
the image.  This will be important to keep in mind when you want to preserve your work and inspect it or send it
to someone else.

## Starting MadGraph
Working from within the image, we will now begin to get a handle for how to use MadGraph.  It is rather
easy, and can be started by going into the `MG5_aMC_v2_6_6` and execute the `mg5_aMC` executable
~~~bash
cd MG5_aMC_v2_6_6
./bin/mg5_aMC
~~~
which will boot up the MadGraph interactive program
~~~
************************************************************
*                                                          *
*                     W E L C O M E to                     *
*              M A D G R A P H 5 _ a M C @ N L O           *
*                                                          *
...
...
...
Defined multiparticle vl = ve vm vt
Defined multiparticle vl~ = ve~ vm~ vt~
Defined multiparticle all = g u c d s u~ c~ d~ s~ a ve vm vt e- mu- ve~ vm~ vt~ e+ mu+ t b t~ b~ z w+ h w- ta- ta+
MG5_aMC>
~~~

If you are new to MadGraph, the best next thing to do is spend some time working through the interactive tutorial
by requesting that it be run from within MadGraph

~~~bash
MG5_aMC> tutorial
~~~

This will give you a hang of the syntax and general workflow that one follows to be able to use a model, in this case the Standard Model.

> ## MG Installs
>
> Note that there are multiple "modules" that can be installed along with MadGraph.
> In this docker image, we have already installed the Pythia module.  Depending on how much you
> look into MadGraph, you may also want to install the detector simulation or analysis packages.
> If you do this locally, and then you exit the image, this will be lost.  However, if you
> find this frustrating and would like it to persist, just ask one of us and we can help you build
> your own docker image with these new modules installed.
>
{: .callout}

## Running DMsimp in MadGraph
Once you are familiar with MadGraph, let's start to use the model that is currently one of the simplest benchmark models
described here [1507.00966](https://arxiv.org/abs/1507.00966) and recommended by the [LHC-DMWG](https://lpcc.web.cern.ch/content/lhc-dm-wg-wg-dark-matter-searches-lhc).
This is a model that introduces a single spin 1 mediator (Z') which couples to both SM fermions and dark matter.
This is the `DMsimp` model and the technical details are described on the MG site - [DMsimp](http://feynrules.irmp.ucl.ac.be/wiki/DMsimp).
If you go here and look for `DMsimp_s_spin1.zip` you will find the UFO ([Universal FeynRules Output](https://arxiv.org/abs/1108.2040))
for this model.  However, this has already been included withing the docker image and you can see it in the `models` directory
within MadGraph.

~~~bash
ls MG5_aMC_v2_6_6/models
~~~

Using this model is rather straightforward and is outlined in the [DMsimp](http://feynrules.irmp.ucl.ac.be/wiki/DMsimp) webpage.
However, for our purposes to keep things simple and uniform we will be generating the monojet signature and using the leading order
generation (because NLO takes even longer).  To do this, start MadGraph and import the model

~~~bash
./bin/mg5_aMC
MG5_aMC>import model DMsimp_s_spin1 --modelname
~~~

from this, you should see all of the additional particles appear that come with this model

~~~
INFO: load particles
INFO: load vertices
Pass the definition of 'j' and 'p' to 5 flavour scheme.
Kept definitions of multiparticles l- / vl / l+ / vl~ unchanged
Defined multiparticle all = g ghg ghg~ u c d s b u~ c~ d~ s~ b~ a gha gha~ ve vm vt e- mu- ve~ vm~ vt~ e+ mu+ t t~ z w+ ghz ghwp ghwm h xr xc y1 w- ghz~ ghwp~ ghwm~ xc~ ta- xd ta+ xd~
~~~

Of particular interest is the `y1` mediator and the `xd` and `xd~` dark matter particles.  Now that this
model is imported, generate the desired monojet signature

~~~bash
MG5_aMC>generate p p > xd xd~ j
~~~

from which you should see a myriad of processes generated

~~~
INFO: Checking for minimal orders which gives processes.
INFO: Please specify coupling orders to bypass this step.
INFO: Trying coupling order WEIGHTED<=5: WEIGTHED IS 2*QED+2*DMV+QCD
INFO: Trying process: g g > xd xd~ g DMV<=2 WEIGHTED<=5 @1
INFO: Trying process: g u > xd xd~ u DMV<=2 WEIGHTED<=5 @1
INFO: Process has 2 diagrams
...
...
...
INFO: Process b~ g > xd xd~ d~ added to mirror process g b~ > xd xd~ d~
INFO: Process b~ g > xd xd~ b~ added to mirror process g b~ > xd xd~ b~
INFO: Process b~ d > xd xd~ g added to mirror process d b~ > xd xd~ g
INFO: Process b~ b > xd xd~ g added to mirror process b b~ > xd xd~ g
21 processes with 42 diagrams generated in 0.442 s
Total: 21 processes with 42 diagrams
MG5_aMC>
~~~

Now perform the `launch` command to start the generation of events

~~~bash
MG5_aMC>launch
~~~

which will output all of this information to a directory, which will by default be named `PROC_DMsimp_s_spin1_0`,
and then bring up a few selection menus where you can modify the running conditions of the generation.  The first
is the option to turn on a parton shower (i.e. Pythia).  It will appear as

~~~
The following switches determine which programs are run:
/=================== Description ===================|============= values ==============|======== other options ========\
| 1. Choose the shower/hadronization program        |        shower = OFF               |     Pythia8                   |
| 2. Choose the detector simulation program         |      detector = Not Avail.        |     Please install module     |
| 3. Choose an analysis package (plot/convert)      |      analysis = Not Avail.        |     Please install module     |
| 4. Decay onshell particles                        |       madspin = OFF               |     ON|onshell                |
| 5. Add weights to events for new hypp.            |      reweight = OFF               |     ON                        |
\=======================================================================================================================/
Either type the switch number (1 to 5) to change its setting,
Set any switch explicitly (e.g. type 'shower=Pythia8' at the prompt)
Type 'help' for the list of all valid option
Type '0', 'auto', 'done' or just press enter when you are done.[60s to answer]
~~~

at first and you should elect to switch the first switch `[1]` by entering 1 and hitting enter.  This will
then indicate the switch has been changed.  Next, it will ask if you wish to modify any of the parameter settings

~~~
Do you want to edit a card (press enter to bypass editing)?
/------------------------------------------------------------\
|  1. param   : param_card.dat                               |
|  2. run     : run_card.dat                                 |
|  3. pythia8 : pythia8_card.dat                             |
\------------------------------------------------------------/
 you can also
   - enter the path to a valid card or banner.
   - use the 'set' command to modify a parameter directly.
     The set option works only for param_card and run_card.
     Type 'help set' for more information on this command.
   - call an external program (ASperGE/MadWidth/...).
     Type 'help' for the list of available command
 [0, done, 1, param, 2, run, 3, pythia8, enter path][90s to answer]
~~~
For now, we will leave these to all of their default values.  Later on, we will need to
understand how these can be modified and what they mean such that we can perform a "parameter scan"
over an entire grid of our parameter space.

After hitting "enter" here, you will see MadGraph start running and produce output information
to the terminal that displays information for both the
matrix element event generation, and then the parton shower generation.  For both of these steps,
the matrix element generation should go rather quickly.  However, it is the parton showering
of the events that takes a considerable amount of time (something like 20 minutes on a MacBook pro from 2014).

### Matrix Element Output - MadGraph

The output here gives you information about how MadGraph organizes the generation of events.  There
are two processes, one for `qg` initiated events and the other for `qq` initiated events.  After the first
pass, you can already see that MadGraph has given you something useful, **the cross section for this process!**
Now, don't worry about having to write this down or anything, it will automatically be stored in the `MG5_aMC_v2_6_6/PROC_DMsimp_s_spin1_0/Events/run_01/run_01_tag_1_banner.txt`
directory, along with other useful information pertaining to this run.  Once this has finished running
take a look at that file if you unfamiliar with its contents.

Also produced by this stage of the simulation is a file called and LHE ([Les Houches Event](https://arxiv.org/pdf/hep-ph/0609017.pdf))
file.  If you look at `MG5_aMC_v2_6_6/PROC_DMsimp_s_spin1_0/Events/run_0/unweighted_events_01.lhe` you will see an XML-formatted
file that contains the four vectors of the Feynman diagrams of the matrix element for each event.  MadGraph takes care of
the internal aspects of this information and you may have to read a bit about LHE files to get a hang of how to parse precisely
what is shown.  However, the main takeway from this is that what is saved here are the outgoing particles, at **parton level**,
before any sort of parton shower or hadronization.  You can already gleem quite a bit of information concerning the kinematics
and signatures of your sample by inspecting this file and perhaps even making some distributions of things like the
vector sum of the transverse momentum of the dark matter particles.  Eventually, it is this which will be reconstructed as
**missing transverse momentum** in the detector.

~~~
INFO: Update the dependent parameter of the param_card.dat
Generating 10000 events with run name run_01
survey  run_01
INFO: compile directory
Not able to open file /contur/MG5_aMC_v2_6_6/PROC_DMsimp_s_spin1_0/crossx.html since no program configured.Please set one in ./input/mg5_configuration.txt
compile Source Directory
Using random number seed offset = 21
INFO: Running Survey
Creating Jobs
Working on SubProcesses
INFO:     P1_gq_xdxdxq
INFO:     P1_qq_xdxdxg
INFO:  Idle: 1,  Running: 0,  Completed: 1 [ current time: 22h17 ]
INFO:  Idle: 0,  Running: 1,  Completed: 1 [ current time: 22h17 ]
INFO:  Idle: 0,  Running: 0,  Completed: 2 [  1.1s  ]
INFO: End survey
refine 10000
Creating Jobs
INFO: Refine results to 10000
INFO: Generating 10000.0 unweigthed events.
INFO: Effective Luminosity 390.350661758 pb^-1
INFO: need to improve 3 channels
Current estimate of cross-section: 30.74159 +- 0.275133382416
    P1_gq_xdxdxq
    P1_qq_xdxdxg
INFO:  Idle: 11,  Running: 2,  Completed: 0 [ current time: 22h17 ]
INFO:  Idle: 8,  Running: 2,  Completed: 3 [  1.7s  ]
INFO:  Idle: 4,  Running: 2,  Completed: 7 [  4.7s  ]
INFO:  Idle: 0,  Running: 2,  Completed: 11 [  8.5s  ]
INFO:  Idle: 0,  Running: 0,  Completed: 13 [  10.6s  ]
INFO: Combining runs
INFO: finish refine
refine 10000
Creating Jobs
INFO: Refine results to 10000
INFO: Generating 10000.0 unweigthed events.
INFO: Effective Luminosity 390.398919376 pb^-1
INFO: need to improve 0 channels
Current estimate of cross-section: 30.73779 +- 0.0838741492883
    P1_gq_xdxdxq
    P1_qq_xdxdxg
INFO:  Idle: 0,  Running: 0,  Completed: 0 [ current time: 22h17 ]
INFO: Combining runs
INFO: finish refine
INFO: Combining Events
  === Results Summary for run: run_01 tag: tag_1 ===

     Cross-section :   30.74 +- 0.08387 pb
     Nb of events :  10000

INFO: Running Systematics computation
INFO: Trying to download NNPDF23_lo_as_0130_qed
Unable to download /cvmfs/sft.cern.ch/lcg/external/lhapdfsets/current/NNPDF23_lo_as_0130_qed.tar.gz
NNPDF23_lo_as_0130_qed.tar.gz:    26.3 MB [1381283400.0%]
INFO: NNPDF23_lo_as_0130_qed successfully downloaded and stored in /usr/local/share/LHAPDF
INFO:  Idle: 0,  Running: 2,  Completed: 0 [ current time: 22h17 ]
INFO:  Idle: 0,  Running: 0,  Completed: 2 [  28.6s  ]
INFO: # events generated with PDF: NNPDF23_lo_as_0130_qed (247000)
INFO: #Will Compute 145 weights per event.
INFO: #***************************************************************************
#
# original cross-section: 30.7347168357
#     scale variation: +14.5% -12.1%
#     central scheme variation: +21.1% -3.34%
# PDF variation: +3.53% -3.53%
#
# dynamical scheme # 1 : 32.3948 +14.9% -12.3% # \sum ET
# dynamical scheme # 2 : 32.3897 +14.9% -12.3% # \sum\sqrt{m^2+pt^2}
# dynamical scheme # 3 : 37.2136 +16% -13% # 0.5 \sum\sqrt{m^2+pt^2}
# dynamical scheme # 4 : 29.7073 +14.2% -11.9% # \sqrt{\hat s}
#***************************************************************************

INFO: End of systematics computation
store_events
INFO: Storing parton level results
INFO: End Parton
reweight -from_cards
decay_events -from_cards
~~~

> ## Make Some Plots
>
> If you fancy yourself a good coder, try to write a short python script that parses this output LHE
> file and uses [matplotlib](https://matplotlib.org/) to make a histogram of the vector sum of the
> transverse momentum of the two dark matter particles.  You can tell which two particles are the DM
> based on their [PdgID](http://pdg.lbl.gov/2007/reviews/montecarlorpp.pdf) values.  Now try to make
> a histogram of the invariant mass of these two particles.
>
> After doing this, think about the following question :
> - How are the distributions of these two variables correlated with the parameters of the model? (Recall : The parameters of the model are stored within the `param_card.dat`)
> - Which of these two variables can we actually reconstruct in an experiment?
>
{: .challenge}

### Parton Shower Output - Pythia

The next stage of simulation (even though it is running "in one go" in this tutorial)
is Pythia.  What is happening here is that the information of the outgoing partons, stored in the output LHE file from
MadGraph, is being passed to a parton shower Monte Carlo generator.  A number of possible generators of this
type are available (i.e. [Pythia](http://home.thep.lu.se/~torbjorn/pythia81html/Welcome.html), [Sherpa](https://sherpa.hepforge.org/), [Herwig](https://herwig.hepforge.org/)) but we have decided to use Pythia as it is
one of the most common ones used at the LHC.  It is also possible to run Pythia as a standalone program
and there are extensive tutorials on the Pythia webpage itself, but that is out of the direct scope of this tutorial.
Luckily, it interfaces nicely to MadGraph and you can simply use it.

But what is it doing? Well, the LHE file contains raw partons, and we know that these particles are colored objects
and due to confinement of QCD, such particles are not stable.  Therefore, when they are produced, they undergo a
two step process that will result in an ensemble of hadrons.  The first is a series of "parton Bremstrahlungs", also
referred to as splittings, in which a quark emits a gluon or a gluon splits to two quarks in a shower-like process.  The physics
that governs this process is that of QCD, but in the limit of small angles and low energy emissions, also referred to
as Soft and Collinear Effective Theory (SCET).  With each splitting, the available energy gets diluted.  This process continues until the energy of the set of partons is low enough that they begin to bind together to form stable hadrons.  The process
by which this binding occurs is not understood from first principle but rather follows an empirical model with a
number of parameters which themselves are tuned to reproduce certain measurements at hadron colliders, such as the number of charged particles produced in an event.  It is possible, however, to change the values of these parmeters yourself and they are stored in the `pythia_card.dat` file ... which you should not have seen (but not changed!) before.

The output of this stage of generation will be a [HEPMC](http://hepmc.web.cern.ch/hepmc/) file which can be found at `MG5_aMC_v2_6_6/PROC_DMsimp_s_spin1_0/Events/run_0/FXME.hepmc`.  This contains similar information to the LHE file, in that
it comes in a standard format and refers to the four momenta of all the outgoing particles from the generation.  However, if you look
at this file manually, it will appear much denser and challenging to read.  Part of the reason is because unlike looking at the
partons from the matrix element process in MadGraph, dozens of outgoing hadrons have been formed so there is a lot of information.
A number of tools (e.g. [HepMCVisual](https://iopscience.iop.org/article/10.1088/1742-6596/219/4/042032)) have been formed to visualize and analyze the information here, including some that can be
installed and used within MadGraph (e.g. [MadAnalysis](https://madanalysis.irmp.ucl.ac.be/)) but using them is out of the scope of this tutorial.  Instead we will
by using the [Rivet]() tool/library which expects as input a `.HEPMC` file ... and you now have one for your Z' process!

~~~
reweight -from_cards
decay_events -from_cards
INFO: Running Pythia8 [arXiv:1410.3012]
Splitting .lhe event file for PY8 parallelization...
Submitting Pythia8 jobs...
Pythia8 shower jobs: 1 Idle, 1 Running, 0 Done [26 seconds]
Pythia8 shower jobs: 0 Idle, 2 Running, 0 Done [5m26s]
Pythia8 shower jobs: 0 Idle, 1 Running, 1 Done [12m50s]
Pythia8 shower jobs: 0 Idle, 0 Running, 2 Done [13m15s]
Merging results from the split PY8 runs...
WARNING: Install gnuplot to be able to view the plots generated at :

INFO: Pythia8 shower finished after 15m18s.
  === Results Summary for run: run_01 tag: tag_1 ===

     Cross-section :   30.74 +- 0.08387 pb
     Nb of events :  10000

INFO: storing files of previous run
INFO: Storing Pythia8 files of previous run
INFO: Done
quit
INFO:
more information in /contur/MG5_aMC_v2_6_6/PROC_DMsimp_s_spin1_0/index.html
~~~

## Generating More Runs

Now that you have generated an ensemble of events, you can proceed to study them with contour (next page).
However, you will invariably be wanting to investigate the various settings in this model to see how
it behaves without the "factory default" settings.  To do that, there are three important pieces to consider.

**[1] Collision Characteristics** (`run_card.dat`) :

When you initially generated a process, you specified
the input and outgoing particles.  However, there are a number of other parameters that are important to
consider (i.e. center of mass energy PDF choice) that must be specified.  And some of them can change the
outcome of the run.  You may want to investigate them, and to do so, you should change the `Cards/run_card.dat`.

**[2] Model Parameters** (`param_card.dat`) :

What if you want to probe a different point in the parameter
space of your model.  For instance, what if you want to change the value of the couplings or the masses of
the particles?  Well, to do this, you will need to modify the `Cards/run_card.dat` file, browsing through to
find the precise line that is associated to the parameter of interest.

Often times you will want to test a series of values for a single parameter in your model, and in this case
there is a nice syntax that can be specified here.  In place of the single number which would be the one value of
the parameter that is tested, you write `scan:[100,200,300]` then for the parameter of interest, MadGraph
will automagically generate one run per parameter in this list.

**[3] Generation Executable** :

It would be fatiguing to have to type this `launch` command every time and
manually press enter through the options.  Not to mention that this is not a very "automated" way to do things.
However, within the `PROC_XXX` directory that you output, there is an executable called `./bin/generate_events`
which does precisely what it says; it generates events.  You can use the `--help` option to get a sense of
how to use it.  However, the main thing to bear in mind is that once you start it, you don't have the
ability to modify how MadGraph+Pythia will run "mid execution".  Therefore, you must have your `param_card.dat`
and `run_card.dat` configured before hand.  Once executing it, the events will be generated and a new `./Events/run_XY`
directory will be generated, like it was in your first run.

At the end of the day, you may end up with a whole lot of `run_XY` directories and you may hesitate and be confused
about how to keep them all straight.  Luckily, within each directory, the `run_XY_tag_1_banner.txt` file
stores the provenance of all the run information for you to parse after the fact.



{% include links.md %}

