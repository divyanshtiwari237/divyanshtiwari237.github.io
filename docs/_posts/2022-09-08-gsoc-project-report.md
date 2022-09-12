---
layout: post
title: "GSoC 2022 Project Report "
date: '2022-09-08 17:20:00 +0530'
categories: open_source
---


## Introduction
The Geant4 toolkit is the basis of the particle transport applications used in High Energy Physics (HEP) experiments, at CERN, other laboratories worldwide and in a large number of diverse applications.A key ability of Geant4 is the propagation of charged particles in electromagnetic fields. A challenging application involves the tracking of particles in accelerators for a large number of turns.Specifically, the muon g-2  experiment at Fermilab seeks to uncover whether a yet undiscovered force influences how the spin of the muon behaves.This requires the use of integration schemes which preserve phase space volume and  energy over the course of the simulation.Currently, none of the numerical integration schemes present in the toolkit are energy preserving.
Hence, the aim of this project is to implement multiple methods which do not accumulate errors in energy and phase space volume over a large number of integration steps.


## Project Details

My project was about implementing symmplectic integrators into the Geant4 codebase.Symplectic integrators are methods that conserve phase space volume. They are excellent for long term accurate tracking of particles.

## Progress:

### Testbed Application:

Before starting my work on the methods themselves, it was imperative to come with Geant4 testbed application that would be used to test these method out. As such I developed a Geant4 application that provides the  flexible choice of using a variety of integrator methods for their easy testing. The work done for this application can be found in the following [Merge Request-1](https://gitlab.cern.ch/geant4/geant4-dev/-/merge_requests/2930) to Geant4 developer repository. The testbed application code was submitted in the following [commit](https://gitlab.cern.ch/geant4/geant4-dev/-/commit/906aec08dfc2eccd6d49109efebfaeebeaae09cd?merge_request_iid=2930) of the Merge Request.Alternatively, the code should be visible in the following [PR-1](https://github.com/Geant4/geant4/pull/48)

### Method-1: The Boris Algorithm:

The first method that we decided to implement was the boris algorithm.The 2nd order method is easy to implement and conservers phase space volume, even though it is not symplectic.The method was implemented along the lines of the following [paper](https://aip.scitation.org/doi/10.1063/1.5051077). The algorithm was implemented by designing a stepper class (`G4BorisScheme`) and a driver class (`G4BorisDriver`).The implementation can be found in the following [Merge Request-1](https://gitlab.cern.ch/geant4/geant4-dev/-/merge_requests/2930).Alternatively, the code should be visible in the following [PR-2](https://github.com/Geant4/geant4/pull/49)

### Method-2: The Boris-SDC (Work in Progress)

After successfully  implementing the 2nd order Boris Algorithm, I worked on implementing a higher order method, namely, Boris-SDC.Boris-SDC was designed to provide a high order alternative to Boris, with strong conservation properties, improved accuracy and lower computational effort required to attain this accuracy.Boris-SDC is fundamentally a collocation method solved via spectral deferred corrections, using the same trick as the Boris algorithm to avoid an implicit velocity dependence.The method was described in detail in the following [thesis](https://etheses.whiterose.ac.uk/22831/1/Smedt%20Thesis%20Final%20v2.pdf) of K. Smedt. The method was implemented in the following [Merge Request-2](https://gitlab.cern.ch/geant4/geant4-dev/-/merge_requests/3029) for the case of a constant magnetic field. It still requires some minor corrections in the UpdateVelocity functions.Alternatively, the code should be visible in the following [PR-3](https://github.com/Geant4/geant4/pull/50)



## Conclusion
Overall I had a highly educative experience this summer and hope to continue contributing to Geant4 in the future.


## Important Links

1. [Mid-Term Report](https://docs.google.com/document/d/1LMNU8qvVKALE9EH1Hc5ROZeL-fl60gFf81KE4QsBj0M/edit?usp=sharing)
2. [Project Proposal](https://docs.google.com/document/d/1gLeoJs8HuCoLsN0AeceiVCH1QyNXHK9V3zmpyA0v0QM/edit?usp=sharing)
3. [Merge Request-1](https://gitlab.cern.ch/geant4/geant4-dev/-/merge_requests/2930)
4. [Merge Request-2](https://gitlab.cern.ch/geant4/geant4-dev/-/merge_requests/3029)
5. [PR-1](https://github.com/Geant4/geant4/pull/48)
6. [PR-2](https://github.com/Geant4/geant4/pull/49)
7. [PR-3](https://github.com/Geant4/geant4/pull/50)
8. [Thesis Used](https://etheses.whiterose.ac.uk/22831/1/Smedt%20Thesis%20Final%20v2.pdf)
9. [Boris Method](https://aip.scitation.org/doi/10.1063/1.5051077)
10. [Work Product Submission](https://docs.google.com/document/d/1p941HeP66Ubo56jffXnzlNsHEQRv72bfRCRtRul1x6U/edit?usp=sharing)