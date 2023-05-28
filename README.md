# KATRIN_Experiment
This project replicates the measurements of the Karlsruhe Trithium Neutrino Experimen (KATRIN) using Monte Carlo data and Data science.

## Introduction

The Neutrino is a fundamental particle, embedded in the Standard Model. They were first postulated by Wolfgang Pauli to explain the missing energy in the energy spectrum of the electron in radioactive $\beta$-decay.  
The occurrence of Neutrino oscillations proves that Neutrinos have mass, as opposed to originally believed. However, these experiments are sensitive to the difference of the squared massed of two mass states and therefore don't show the absolute mass scale of the Neutrino.  
The Karlsruhe Tritium Neutrino (KATRIN) experiment attempts to measure the mass of neutrinos with precision.  
This notebook attempts to replicate the results of the KATRIN experiment by first using a simplified model of the Tritium $\beta$-decay spectrum that is unique to KATRIN with Monte Carlo Data and then using basics of Data Analysis to set an upper and lower bound to the neutrino mass to evaluate the sensitivity of the experiment.

**NOTE**:  
The KATRIN experiment uses Tritium in its molecular form, therefor the daughter molecule in the $\beta$-decay can be in a rotational-vibrational or electronically excited state which lowers the effective energy of the electron and neutrino and shifts the endpoint. Tritium molecules in the source are also in thermal motion and can experience the Doppler effect and broaden the differential spectrum. Lastly, we have to account for potential energy losses in inelastic scattering process in the source.
I will neglect these effects to save computational time, but we will see that it still returns values close to what the real Katrin experiment measures.

## Overview: Models and Mathematics

'''math
    E_{tot} = E + m_{e}  \text{total electron energy}\\
    p = \sqrt{E^{2}_{tot} - m^{2}_{e}} \text{electron momentum}\\
    \beta = \frac{E_{tot}}{p} \text{relativistic beta factor}\\
    \eta = \frac{2\cdot a}{\beta} \text{number of protons in $T_{2}$, fine structure 
            constant $\alpha$} \\
    \end{aligned}
\end{equation*}
'''

**Fermi function**
$$
    F(Z',E) = \frac{2\pi \eta}{1-e^{-2\pi \eta}}\cdot (1.002037 - 0.001427\beta)
$$

**Differential Spectrum**
$$
    \frac{d\Gamma}{dE} = C\cdot F(Z',E)\cdot p\cdot (E+m_{e})\cdot \left(E-E_0\right) \cdot \sqrt{\left(E-E_0\right)^{2} - m_{\nu}^{2}}\cdot \Theta(E_0 - E - m_{\nu})
$$

**Transmission function**
$$
    T(qU,E) =
    \begin{cases}
      0& \text {$E<qU$} \\ 
      \frac{1-\sqrt{1-f\cdot \frac{B_{source}}{B_{ana}}\frac{E-qU}{E}} }{1-\sqrt{1-\frac{B_{source}}{B_{ana}}}}& \text{$qU\leq E\leq qU\frac{f\cdot B_{max}}{f\cdot B_{max}-B_{ana}}$} \\
      1& \text{$E>qU\frac{f\cdot B_{max}}{f\cdot B_{max}-B_{ana}}$}
    \end{cases}
$$

$$
    \text{with } f = \frac{\frac{E-qU}{m_e}+2}{\frac{E}{m_e}+2}\ .
$$

### Models

**Integral Model**
$$
    R(qU) = N\cdot \int_{qU}^{E_{0}} \frac{d\Gamma}{dE}(E;m_{\nu}^{2},E_{0})\cdot T(qU,E) \,dE + B,
$$

**Differential Modell**
$$
    M(E) = N\cdot \frac{d\Gamma}{dE}(E; m_\nu^2,E_0) + B\ ,
$$
