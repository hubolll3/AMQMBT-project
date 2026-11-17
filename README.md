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

These quantities need not agree. In particular, an apparent enhancement
of ferromagnetic correlations in a selected ensemble should not
automatically be interpreted as the generation of ferromagnetism in the
unconditioned system.

## Physical model

We consider the repulsive Fermi--Hubbard Hamiltonian

\[ H\_{`\mathrm{Hub}`{=tex}} = -`\sum`{=tex}*{`\langle `{=tex}i
j`\rangle`{=tex},`\sigma`{=tex}}
t*{ij}`\left`{=tex}(c\^`\dagger`{=tex}*{i`\sigma`{=tex}}c*{j`\sigma`{=tex}}+`\mathrm{h.c.}`{=tex}`\right`{=tex}) +
U`\sum`{=tex}*i
`\left`{=tex}(n*{i`\uparrow`{=tex}}-`\frac{1}{2}`{=tex}`\right`{=tex})
`\left`{=tex}(n\_{i`\downarrow`{=tex}}-`\frac{1}{2}`{=tex}`\right`{=tex})
-`\mu`{=tex}`\sum`{=tex}\_i n_i , \]

with (U\>0), where (c\_{i`\sigma`{=tex}}) and
(c\^`\dagger`{=tex}*{i`\sigma`{=tex}}) annihilate and create a fermion
of spin (`\sigma`{=tex}) on site (i), and
(n_i=n*{i`\uparrow`{=tex}}+n\_{i`\downarrow`{=tex}}).

The on-site pair-loss jump operators are

\[
L_j=`\sqrt{2\gamma}`{=tex},c\_{j`\downarrow`{=tex}}c\_{j`\uparrow`{=tex}},
\]

where (`\gamma`{=tex}) is the pair-loss rate. The density matrix obeys

\[ `\frac{d\rho}{dt}`{=tex} =
-i\[H\_{`\mathrm{Hub}`{=tex}},`\rho`{=tex}\] + `\sum`{=tex}\_j
`\left`{=tex}( L_j`\rho `{=tex}L_j\^`\dagger`{=tex}
-`\frac{1}{2}`{=tex}{L_j\^`\dagger `{=tex}L_j,`\rho`{=tex}}
`\right`{=tex}). \]

The project starts from one fermion per site. The project specification
notes that the reference work by Nakagawa *et al.* uses the unshifted
interaction convention. For the stated initial states and trajectories,
the difference is a constant plus a particle-number term and does not
change the correlations or loss probabilities.

Throughout, state the lattice geometry, boundary conditions, and energy
units explicitly. Use (`\hbar`{=tex}=k\_{`\mathrm `{=tex}B}=1).

## Project goals

The project is organized around three main questions.

### 1. Quantum trajectories and the loss mechanism

-   Derive the effective non-Hermitian Hamiltonian governing evolution
    between jumps.
-   Derive the jump probabilities and the post-jump state.
-   Distinguish no-loss evolution from the unconditioned Lindblad
    ensemble.
-   Use the strong-coupling spin picture to explain the role of virtual
    doublons and spin-dependent lifetimes.

### 2. MPS simulations and validation

-   Explain the Schmidt decomposition and the MPS representation.
-   Describe the truncation procedure and its effect on time evolution.
-   Simulate quantum trajectories, including stochastic jumps, for an
    interacting chain beyond a dimer.
-   Validate the implementation against an exact calculation for a small
    system.
-   Reproduce one published many-site result.
-   Assess errors due to time-step size, MPS bond dimension, and
    trajectory sampling. In particular, document how jump probabilities
    are handled during normalization and truncation.

### 3. Magnetic correlations and conditioning

Compare the following observables or ensembles:

-   Unconditional spin correlations.
-   Spin correlations conditioned on no loss.
-   Occupancy-conditioned spin correlations, where both measured sites
    are required to be singly occupied.

Also:

-   Report particle survival and conditioning probabilities.
-   Compare an initial Néel product state with a product of
    nearest-neighbour spin singlets on a small chain.
-   Derive the constraint on total-spin-sector populations in the
    unconditioned ensemble.
-   Check
    (`\langle `{=tex}`\mathbf{S}`{=tex}\_{`\mathrm{tot}`{=tex}}\^2`\rangle`{=tex})
    and explain what changes under conditioning.
-   Qualify any claim that particle loss produces ferromagnetism.

## Suggested workflow

The following sequence follows the project brief and is intended as a
practical starting point.

1.  **Establish conventions.** Specify the Hamiltonian, hopping,
    interaction, loss rate, chain length, boundary conditions, initial
    state, and units.
2.  **Derive the trajectory equations.** Work out the effective
    non-Hermitian evolution, jump probabilities, and state update after
    a jump.
3.  **Implement a dimer benchmark.** Compare the trajectory results with
    an exact small-system calculation.
4.  **Extend to a short chain.** Implement MPS time evolution with
    stochastic jumps and compare against exact results wherever
    feasible.
5.  **Validate against the literature.** Use selected fermionic curves
    in Figs. 3--4 of Nakagawa *et al.* as benchmarks. Their eight-site
    calculation is a useful target. Match the reference boundary
    conditions for quantitative comparisons.
6.  **Study correlations and conditioning.** Evaluate the different
    spin-correlation ensembles, survival probabilities, and total-spin
    diagnostics.
7.  **Investigate one extension.** Possible directions from the brief
    include weak local spin dephasing or comparing constant loss with a
    finite loss pulse. Compare protocols at a common observation time
    and account for particle survival.

Open chains are convenient for MPS calculations, but any change from the
reference geometry or boundary conditions should be stated explicitly
and validated against the same geometry.

## Numerical methods

### Quantum trajectories

For each trajectory, evolve the state under the effective non-Hermitian
Hamiltonian between stochastic quantum jumps. At a jump, apply the
relevant (L_j) and update the state. The ensemble of trajectories
represents the Lindblad evolution when sampled and averaged
appropriately.

The implementation should document:

-   The convention used for the time-step jump probabilities.
-   How the no-jump state is normalized.
-   How jump probabilities are computed and sampled.
-   How the state is updated after a jump.
-   Whether normalization and MPS truncation occur before or after
    probability evaluation, and how this is controlled.

### Matrix product states

Represent the many-body wavefunction as an MPS and control its size
through a specified bond-dimension and truncation criterion. Report
convergence with respect to:

-   Time step.
-   Maximum bond dimension.
-   Truncation tolerance (if used).
-   Number of sampled trajectories.

The project brief encourages established libraries such as
[ITensorMPS](https://github.com/ITensor/ITensorMPS). The repository
should identify the actual software and version used.

## Validation and error analysis

At minimum, the numerical study should include:

-   An exact small-system comparison, beginning with a dimer and
    extending to a short chain where possible.
-   Reproduction of one published many-site result.
-   Time-step convergence.
-   Bond-dimension and truncation convergence.
-   Trajectory-sampling uncertainty.
-   A clear account of particle survival and conditioning probabilities.

Separate numerical errors from physical effects introduced by
conditioning or by changing the geometry and boundary conditions.

## Repository structure

The structure below is a suggested organization. Adapt it to the
implementation in this repository.

``` text
.
├── README.md
├── src/                  # Hamiltonian, trajectory and MPS implementation
├── scripts/              # Reproducible simulation and analysis entry points
├── notebooks/            # Exploratory analysis and figures
├── data/
│   ├── raw/              # Raw simulation output (if tracked)
│   └── processed/        # Processed data (if tracked)
├── figures/              # Figures generated from the analysis
├── tests/                # Small-system and regression tests
└── environment.yml       # Or requirements.txt / Project.toml, as applicable
```

Do not commit large generated datasets unless appropriate for the
repository. If data are stored externally, document where they can be
obtained and how to regenerate them.

## Getting started

Add the installation and execution instructions for the software used in
this repository. For example:

``` bash
git clone <repository-url>
cd <repository-directory>

# Install the dependencies using the environment file provided by this project.
# For example:
conda env create -f environment.yml
conda activate <environment-name>
```

Then document the actual commands used to run the simulations and
reproduce the figures. Replace the placeholders below with the entry
points implemented in this repository:

``` bash
# Example placeholders — replace with the actual commands.
python scripts/run_dimer.py
python scripts/run_chain.py
python scripts/analyze_results.py
```

## Results

This section should summarize the results obtained by the
implementation, rather than anticipated outcomes. Suggested items to
report:

-   Time evolution of spin correlations for the different trajectory
    ensembles.
-   Particle survival and occupancy-conditioning probabilities.
-   Comparison between Néel and nearest-neighbour singlet initial
    states.
-   The behaviour of
    (`\langle `{=tex}`\mathbf{S}`{=tex}\_{`\mathrm{tot}`{=tex}}\^2`\rangle`{=tex}).
-   Exact-versus-MPS validation and convergence tests.
-   Comparison with the selected literature benchmark.

Add figures with captions that specify the system size, boundary
conditions, parameters, initial state, and ensemble/conditioning used.

## References

1.  M. Nakagawa *et al.*, "Dynamical Sign Reversal of Magnetic
    Correlations in Dissipative Hubbard Models," *Physical Review
    Letters* **124**, 147203 (2020).
    <https://doi.org/10.1103/PhysRevLett.124.147203>\
    Main reference for the loss mechanism and fermionic many-site
    benchmarks.

2.  A. J. Daley, "Quantum trajectories and open many-body quantum
    systems," *Advances in Physics* **63**, 77 (2014).\
    Background on quantum trajectories and their implementation in
    many-body systems.

3.  U. Schollwöck, "The density-matrix renormalization group in the age
    of matrix product states," *Annals of Physics* **326**, 96 (2011).\
    Background on MPS, truncation, and time evolution.

4.  M. Foss-Feig *et al.*, "Steady-State Many-Body Entanglement of Hot
    Reactive Fermions," *Physical Review Letters* **109**, 230501
    (2012).\
    Background on spin conservation and constraints associated with
    particle loss.

## Reproducibility

This repository should contain, or point to, the software and data
needed to regenerate the reported figures. Record software versions,
parameter choices, random seeds where relevant, and concise reproduction
commands. Cite external software and comply with its licence.

If AI tools are used for literature exploration, derivations,
programming, debugging, or writing, include a brief statement in the
project report describing the tools' contributions and how the work was
checked.

## Authors and contributions

-   **Authors:** TODO
-   **Contributions:** TODO

------------------------------------------------------------------------

*This README describes the scope and requirements of Project 3 in the
AMQMB HS2026 project brief. Implementation-specific details, commands,
parameters, and numerical findings should be filled in to match the
actual repository.*
