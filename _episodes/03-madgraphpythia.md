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
Booting up the image and describing the inner workings and how it links to your local machine

## Starting MadGraph
Guide them to start MadGraph

callout for the self-guided tutorial

## Running DMsimp in MadGraph
step by step guide

## The Output

### MadGraph : LHE Files
Guide them through inspecting the LHE file that comes out of madgraph

### MadGraph+Pythia : HEPMC Files
Describe what comes out of the HEPMC file

How can they inspect HEPMC files?

## Changing Model Parameters
Describe the param card and have them change the mediator mass

## Changing Running Parameters
Describe the run card and have them change the input particle type


{% include links.md %}

