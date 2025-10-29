# Calcium-based Synaptic Plasticity in NESTML

Project replicating the spike-timing-dependent plasticity (STDP) framework proposed by **[Chindemi et al. (2022)](https://doi.org/10.1038/s41467-022-30214-w)** inside the **NESTML** simulation environment.

## Project Overview

Synaptic plasticity is the ability of synapses to strengthen or weaken over time as a function of spike timing. The calcium-control hypothesis suggests that postsynaptic calcium dynamics determine whether long-term potentiation (LTP) or long-term depression (LTD) occurs.

In this project, we modeled neurons and synapses in NESTML/PyNestML to reproduce the calcium-based STDP mechanism:

- **Neuron model:**  
  Based on the Hill–Tononi point-neuron formalism, simplified for computational efficiency while retaining key synaptic currents (AMPA, NMDA).  

- **Synapse model:**  
  Custom implementation of calcium-dependent plasticity. Calcium influx is modeled through:  
  - NMDA receptor current (including magnesium block),  
  - Voltage-dependent calcium channels (VDCC, after Chindemi et al.).

- **Plasticity mechanism:**  
  - Calcium traces integrated through a leaky accumulator (*c⋆*, per Chindemi et al.).  
  - Synaptic efficacy (ρ) updated once potentiation or depression thresholds are crossed.  
  - ρ modulates AMPA conductance and presynaptic release probability.  
  - Vesicle release simplified from the original stochastic model to a mean weight with Gaussian noise.

## Key Behaviors

- **Pre-before-post spiking:**  
  Temporal alignment of NMDA receptor activation with postsynaptic depolarization produces supralinear calcium transients, leading to LTP.  

- **Post-before-pre spiking:**  
  Misaligned events yield smaller calcium transients, sufficient only for LTD.  

- **Frequency dependence:**  
  Longer NMDA-mediated calcium events dominate shorter VDCC ones, captured by the leaky calcium integrator.  

## Contents

- `mhill_tononi_neuron.nestml` — NESTML implementation of the neuron model.  
- `stdp_ca_synapse.nestml` — NESTML implementation of the calcium-based STDP synapse.
- `notebook.ipynb` — Jupyter notebook with the simulations.
- `supplementary_material.pdf` — Comments on findings.
