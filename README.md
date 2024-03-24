# KATRIN_Experiment
This monte-carlo simulation project replicates the measurements of the Karlsruhe Tritium Neutrino experiment (KATRIN) using Monte Carlo data and Data science.  

## Introduction

The Neutrino is a fundamental particle, embedded in the Standard Model. They were first postulated by Wolfgang Pauli to explain the missing energy in the energy spectrum of the electron in radioactive $\beta$-decay.  
The occurrence of Neutrino oscillations proves that Neutrinos have mass, as opposed to originally believed. However, these experiments are sensitive to the difference of the squared massed of two mass states and therefore don't show the absolute mass scale of the Neutrino.  
The Karlsruhe Tritium Neutrino (KATRIN) experiment attempts to measure the mass of neutrinos with precision.  
This notebook attempts to replicate the results of the KATRIN experiment by first using a simplified model of the Tritium $\beta$-decay spectrum that is unique to KATRIN with Monte Carlo Data and then using basics of Data Analysis to set an upper and lower bound to the neutrino mass to evaluate the sensitivity of the experiment.

**NOTE**:  
The KATRIN experiment uses Tritium in its molecular form, therefor the daughter molecule in the $\beta$-decay can be in a rotational-vibrational or electronically excited state which lowers the effective energy of the electron and neutrino and shifts the endpoint. Tritium molecules in the source are also in thermal motion and can experience the Doppler effect and broaden the differential spectrum. Lastly, we have to account for potential energy losses in inelastic scattering process in the source.
I will neglect these effects to save computational time, but we will see that it still returns values close to what the real Katrin experiment measures.

## Overview: Models and Mathematics

The models and mathematics can be found in the jupyter notebook.

## Usage
For this project a anaconda/miniconda3 is needed to build a local conda environment on your local system.
```bash
cd conda
conda env create
conda env create -f environment.yml
conda activate neutrino
```
You can then open the Jupyter Notebook and run the individual cells one-by-one. Note that the simulation  
can take a very long time to execute at the step, where $10^5$ random poisson distribution are generated 
(On the author's machine this process took ~3 hours).  

If you want to remove the environment
```bash
conda remove --name neutrino --all
```
