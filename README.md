# Solitary Laser Simulation: With and Without Self-Feedback

## Repository Origin

This repository is a fork of the original work by [Godwin Dian](https://github.com/godwinduan/lasersim). The foundational simulation framework, rate equation implementations, and numerical methods were developed by Godwin and the broader research group. This work would not have been possible without the extensive groundwork laid by Godwin and the contributions of the entire lab.

## Acknowledgments

This project builds directly on the work of:

- **Godwin Dian**
- **Chixuan Chen**
- **Mark Lancaster**
- **Claire Gmachl**

The Lang-Kobayashi rate equation implementations, numerical solver configurations, and physical parameter sets used here were established through their collaborative efforts. Any extensions or modifications in this repository stand on their work.

## Recent Additions

This fork extends the original framework with additional analysis focused on solitary laser behavior with and without self-feedback. The main additions are documented in `solitary_laser_self_feedback.ipynb` and include:

### Enhanced Time Series Analysis

- **Comprehensive time series visualization**:

  - Optical intensity E²(t) evolution at multiple current values
  - Carrier density N(t) dynamics across operating regimes
  - Phase space trajectories (E² vs N scatter plots)
  - Mean intensity and carrier density versus current (dual-axis plot)

- **Multi-current analysis**: Time series data is collected and visualized for several current values spanning below threshold, at threshold, and above threshold, allowing direct comparison of laser dynamics across operating regimes.

### Statistical Analysis and Distributions

- **Carrier density distributions**: Showing the statistical distribution of carrier density at different operating points, revealing the transition from below-threshold to above-threshold behavior.

## Overview

This project simulates the behavior of a semiconductor laser diode, both in isolation and when its own light is reflected back into the laser cavity (self-feedback). The simulation focuses on understanding how laser output power changes with input current, particularly identifying the threshold, linear, and saturation regions that are crucial for laser operation and machine learning applications.

### Scenario 1: Solitary Laser (No Feedback)

A laser operating in isolation - its light exits the device and doesn't return. This is the baseline case.

**What we measure:**

- How output power (intensity) changes with input current
- The "threshold current" - the minimum current needed for lasing
- The relationship between carrier density and light output

### Scenario 2: Laser with Self-Feedback

The laser's own light is reflected back into the cavity (e.g., by a mirror, fiber end, or chip edge). This creates a feedback loop that can dramatically change laser behavior.

**What we measure:**

- How feedback affects the threshold current
- Changes in output power characteristics
- The impact of feedback strength, delay, and phase

## The Physics: Rate Equations

The simulation uses **rate equations** - mathematical models that describe how three key quantities evolve over time:

1. **x(t)** - Real part of the electric field
2. **y(t)** - Imaginary part of the electric field
3. **N(t)** - Carrier density (number of excited carriers)

### Without Feedback (Simpler Case)

The equations describe:

- How the electric field grows or decays based on gain vs. losses
- How carriers are injected, recombine, and are consumed by stimulated emission
- How gain depends on carrier density and light intensity

### With Feedback (More Complex)

Additional terms account for:

- **Delayed feedback**: Light that left the cavity returns after a delay (τf)
- **Feedback strength**: How much light is reflected back (kf)
- **Feedback phase**: The phase relationship between outgoing and returning light (φf)

This creates a **delay differential equation (DDE)** - the current state depends on past states, making the dynamics richer and potentially chaotic.

## Troubleshooting

### Memory Issues

- The simulation stores time series data
- If memory is limited, reduce:
  - Number of current points (n_points)
  - Number of kf values
  - Sampling time (T_sample)

### Convergence Issues

- If results look unstable:
  - Increase transient time (T_trans)
  - Increase sampling time (T_sample)
  - Check that time step (dt) is small enough
