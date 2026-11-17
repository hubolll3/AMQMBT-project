# Loss-Induced Magnetism in the Fermi--Hubbard Model

Numerical study of how on-site particle loss changes magnetic
correlations in an interacting fermionic chain, using Lindblad dynamics,
quantum trajectories, and matrix product states (MPS).

> **Course project:** Advanced Methods in Quantum Many-Body Theory, ETH
> Zürich --- HS 2026\
> **Project 3:** *Loss-induced magnetism with Lindblad dynamics and MPS*

## Overview

This project investigates how particle loss affects magnetic
correlations among the fermions that remain in a one-dimensional
Fermi--Hubbard system.

The system is governed by the repulsive Hubbard Hamiltonian at chemical
potential (`\mu=0`{=tex}), supplemented by on-site two-particle (pair)
loss. The dynamics are described by a Lindblad master equation. Quantum
trajectories provide a stochastic unraveling of this evolution, while
matrix product states make it possible to simulate interacting chains
beyond the small systems accessible to exact diagonalization.

A central focus is the distinction between:

-   **Unconditioned dynamics:** averaging over all quantum trajectories,
    including trajectories in which loss events occur.
-   **No-loss dynamics:** evolution conditioned on observing no loss
    events.
-   **Occupancy-conditioned correlations:** spin correlations evaluated
    only when both measured sites are singly occupied.

