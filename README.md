# Project 1: Quantum Walks and Monte Carlo

**Team Name:** QWalk

**Team Member:** Gaël-Pacôme Nguimeya Tematio  |  **WISER Enrollment ID:** gst-KYZFrwa3eeh0Yov

## Summary

This project investigates how quantum circuits can emulate a Galton Box style Monte Carlo process and related quantum walks, following the [Universal Statistical Simulator](https://arxiv.org/abs/2202.01735) reference. The core idea is to realize a generalized L layer quantum Galton board (QGB) that routes a single 1 hot token across a channel register under the control of a reusable coin qubit. At each layer, a Hadamard on the coin followed by a controlled SWAP sweep spreads amplitude to adjacent channels, and a mid circuit reset recycles the coin. Measuring the channel qubits yields one Monte Carlo sample per shot. This construction provides a clear, modular template for mapping sampling problems onto quantum hardware and for studying the interface between quantum walks and classical Monte Carlo.

The work proceeds through five tasks. **Task 1** reviews the target paper and distills a concise implementation guide for QGBs, focusing on register layout, the per layer routing sweep, and the reuse of a single coin qubit. **Task 2** extends starter code for 1 and 2 layers to a general algorithm that builds circuits for any number of layers L. The implementation uses a structured indexing scheme with 2(L+1) qubits in total, odd indices as measurable bins, and even indices as routing rails. The coin is reset after each layer except the last to keep depth and qubit count low. The analysis pipeline converts raw bitstrings to bin indices, plots histograms, and compares them with the classical binomial reference. A block sum rescaling procedure (for example, grouping shots in blocks of size 8) demonstrates the expected Gaussian behavior from the central limit effect. **Task 3** adds two alternative targets using a noiseless all to all sampler: an exponential distribution and a 1D Hadamard quantum walk. The exponential sampler validates shape and decay against a theoretical curve, while the Hadamard walk demonstrates the characteristic interference pattern for a fixed number of steps. **Task 4** focuses on practical optimization under noise models by keeping the circuit template simple (single reusable coin, CSWAP based routing, optional barriers for readability) and by separating the algorithmic layer from backend specific transpilation. **Task 5** quantifies agreement between measured and target distributions using statistical distance measures and uncertainty aware reporting, complementing visual checks.

Results for L = 4 illustrate the end to end flow. The rescaled QGB histogram closely tracks a Gaussian fit, the exponential sampler matches its expected decay, and the Hadamard walk reproduces the predicted distribution for a chosen step count. These examples confirm the correctness and modularity of the approach and provide a solid baseline for scaling studies.

The main limitation encountered is computational resources for larger L and higher shot counts, which impact both simulation time and statistical precision. Future work includes scaling L, integrating backend specific noise models and decompositions for CSWAP, exploring unitary clean up in place of reset where advantageous, adding per row bias schedules for shaped targets, and executing small L runs on hardware with error mitigation. Overall, the repository offers a reusable QGB template, analysis utilities, and example studies that can support both education and benchmarking in quantum sampling workflows.

## Project Presentation Deck

[project-presentation-deck.pdf](./project-presentation-deck.pdf)
