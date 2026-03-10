# Introduction to Molecular Dynamics Simulations

### Chemical Simulations 

##### Why work with computer-aided methods?
The main goal of computer-aided methods in chemistry and material design is to obtain information about chemical system by modeling atoms, molecules and ions on the computer.

##### Advantages of computer-aided methods:
- Cost-effective
- Possibility of studying systems of interest on the atomic level
- Ability to simulate conditions that are difficult to achieve experimentally

#### Energy and Forces
When we perform a simulation of a chemical system, we are interested in the **energy** and **forces** acting on the atoms. The energy of a system is a function of the positions of all atoms in the system.[1](https://levich.ccny.cuny.edu/koplik/molecular_simulation/AT2.pdf).

The forces acting on each atom are related to the energy by the following equation:

$$ F_i = - \frac{\partial E}{\partial r_i} $$

where $$ F_i $$ is the force acting on atom $$ i $$ , $$ E $$ is the total energy of the system, and $$ r_i $$ is the position of atom $$ i $$.

The level of theory used to calculate the energy and forces determines the accuracy and computational cost of the simulation.

There are two main approaches to calculate the energy and forces: Molecular Mechanics (MM) and Quantum Mechanics (QM).

**Difference of Quantum Mechanics (QM) and Molecular Mechanics (MM)**

| Quantum Mechanics (QM) | Molecular Mechanics (MM)("Force Fields") |
| ----------- | ----------- |
|  Based on numerical solutions of Schrödinger's equation to model the electron density of the system: | Based on parametrised potential functions: |
|$$ \hat{H} \Psi = E \Psi $$ | $$ E_{total} = E_{bonded} + E_{non-bonded} $$ |
|  Accurate but computationally expensive (inclusion of - polarisation, charge-transfer effects, many body effects) | fast computationally (needs parameterisation) |


#### Molecular mechanics (MM)/Force Fields (FFs)
Synonyms: 
- molecular mechanics (MM)
- empirical potentials, potential model
- classical approach, classical treatment
- but not: *Molecular Modelling*!

The main idea of MM is to describe molecular interactions via empirical, parametrised potential function.

MM estimates the potential energy of the system by ignoring the electronic motion and considering the positions of nuclei. 

It models atoms as *spheres* and bonds as *springs*, and the potential energy of the system is calculated based on the **bond stretching**, **angle bending**, **dihedral angle** interaction, and **non-bonded** contributions between the atoms in the system. 

[Hooke’s law](https://en.wikipedia.org/wiki/Hooke%27s_law) is typically used to define bond stretching and angle bending. The typical form of FFs (i.e., functional form) to describe the intra- and intermolecular potential energy function of a collection of atoms in the system can be expressed as:

<p align="center">
  <img src="{{ '/figure/FFs.png' | relative_url }}" alt="Force Field" width="auto">
</p>

where the first four terms represent the bonded interactions (bond stretching, angle bending, dihedral angle torsion, and improper dihedral angle torsion), and the last two terms represent the non-bonded interactions (van der Waals and electrostatic interactions).

The well-known [Lennard-Jones](https://en.wikipedia.org/wiki/Lennard-Jones_potential) potential energy function is employed to describe the van der Waals interaction between two atoms in the system which is given by:

$$ E_{LJ} = 4 \epsilon \left[ \left( \frac{\sigma}{r} \right)^{12} - \left( \frac{\sigma}{r} \right)^{6} \right] $$

where $$  r $$ is the distance between two atoms, $$  \epsilon $$ is the depth of the potential well, and $$  \sigma $$ is the distance at which the potential energy is zero.


##### Molecular Dynamics (MD) Simulations
Description of the time evolution of chemical systems by propagation the Newton's equations of motion. 
How to simulate the dynamics?
The taylor series expansion for *a* = *t* and *x* = *t* + $\Delta t$ is

<p align="center">
  <img src="{{ '/figure/taylor.png' | relative_url }}" alt="Taylor series 1" width="600">
</p>
The big *O* is asymptotic notation that represents the order of approximation. Since velocity is the change in position over time and acceleration is the change in velocity over time, the above expression can be substituted with
<p align="center">
  <img src="{{ '/figure/taylor_2.png' | relative_url }}" alt="Taylor series 1" width="600">
</p>
Numerical evaluation of Taylor expansion 
#### Integrating Equation of Motion



#### Choosing a timestep
In MD simulation, time step ($\Delta t$) 
To improve the efficiency of atomistic MD simulations, it is essential to implement a larger time step $\Delta t$.
However, $\Delta t$ is limited by the fastest motion in the system that is generally associated with the vibrational modes of the lightest atoms in the system, typically hydrogen.

Constraint dynamic approach has been developed to overcome the time step limitation by constraining the degrees of freedom e.g. bond length of `X-H` bonds (with X = C, N, O).
This approach uses Lagrangian multipliers to depict the magnitudes of forces directed along the bonds, ensuring the bond length remains constant.
The SHAKE/RATTLE algorithm can be implemented by applying the bond constraints on high vibrational covalent bond lengths e.g., `C-H`, `C-C` to their average bond length, allowing the use of larger time steps up to 2 fs in the simulation.
The computational time can be reduced by a factor of 5-10 if constrained MD algorithms are applied.

#### Periodic Boundary Conditions (PBC)
In MD simulation, systems are treated as if they were surrounded by their identical copies in all directions.
<p align="center">
  <img src="{{ '/figure/pbc_1.png' | relative_url }}" alt="Periodic Boundary Condition" width="500">
</p>

The figure depicts representation of a three-dimensional periodic system. The simulation box is represented by a cubic box of length *L*. The cubic box is surrounded by its identical copies. **A** particle, marked in green within the central box, can exit the box through the surface of the box. Upon leaving, its periodic image will reappear, entering from the opposite side.

This approach also considers the **minimum image convention**, which means that each particle only interacts with the nearest image of every other particle (either the original particle or one of its periodic images).

#### Temperature and Pressure Scaling
Molecular dynamics simulations can be carried out using several conditions or ensembles. It requires the use of algorithms that generate a thermodynamic ensemble at constant temperatures known as **thermostats**[[2]](https://www.eng.uc.edu/~beaucag/Classes/AdvancedMaterialsThermodynamics/Books/%5BComputational%20science%20(San%20Diego,%20Calif.)%5D%20Daan%20Frenkel_%20Berend%20Smit%20-%20Understanding%20molecular%20simulation%20_%20from%20algorithms%20to%20applications%20(2002,%20Academic%20Press%20)%20-%20libgen.lc.pdf)

The idea of using thermostats in MD simulation can be for several reasons, e.g., to match with experimental conditions, to make a conformational search faster, or to investigate temperature-dependent processes.

Different types of ensembles can describe the system in molecular dynamics, including the microcanonical, canonical, and isothermal-isobaric ensembles.

**Microcanonical Ensemble (NVE)** describes a system where the number of particles, volume, and energy are constant, representing an isolated system without the exchange of particles or energy with its surroundings.

**Canonical Ensemble (NVT)** applies to a system maintaining constant numbers of particles, volume, and temperature. It acts as a closed system in thermal equilibrium with a heat bath at a constant temperature *T*, allowing for energy exchange.

**Isothermal-Isobaric Ensemble (NPT)** defines a system with a constant number of particles, pressure and temperature. It depicts the system in contact with a heat bath at constant temperature *T* and pressure *P*, capable of exchanging energy and volume with the system. At thermal equilibrium, the total energy *E* and volume *V* fluctuate, whereas the number of particles *N* remains constant.

#### Radial Distribution Function (RDF)/Pair Distribution
The radial distribution function, g(r), describes the number of atoms in a shell $$ \Delta r $$ at a distance *r* from a central species/atom. 

The simplest RDF criterion is based on the cutoff or distance criterion.[[3]](https://pubs.acs.org/doi/full/10.1021/acs.jctc.4c00162)

It provides information about the structure of liquids and amorphous solids by describing how particle density varies as a function of distance from a reference particle. 

<p align="center">
  <img src="{{ '/figure/GC.png' | relative_url }}" alt="RDF" width="auto">
</p>

The RDF depicted in the figure above represents the probablity to find a solvent molecule *j* at a spesific distance *r* from a central solute molecule *i*. 

<p align="center">
  <img src="{{ '/figure/h2o_rdf.png' | relative_url }}" alt="RDF_h2o" width="auto">
</p>

The figure above shows RDFs of O-O, O-H, and H-H pairs in pure water.[[3]](https://pubs.acs.org/doi/full/10.1021/acs.jctc.4c00162)

##### Molecular Dynamics (MD) Simulations: Simulation Protocol
MD simulations follows this workflow.
<p align="center">
  <img src="{{ '/figure/loop.png' | relative_url }}" alt="MD simulation workflow" width="600">
</p>

<p align="center">
  <img src="{{ '/figure/integration.png' | relative_url }}" alt="Integration of Newton's equations of motion" width="300">
</p>

The simulation protocol should consider this sequence:
1. Generating initial structure: chemically meaningful structure (no overlapping atoms, correct distances)
2. Generating initial velocities: random according to a Maxwell-Boltxmann distribution at a chosen temperature.
3. Equilibration Phase
4. Production phase

**References**

1. Allen, M. P., & Tildesley, D. J. (2017). *Computer Simulation of Liquids (2nd ed.)*. Oxford University Press [(Chapter 1 & 3 for MD)](https://levich.ccny.cuny.edu/koplik/molecular_simulation/AT2.pdf)

2. Frenkel, D., & Smit, B. (2002). *Understanding Molecular Simulation: From Algorithms to Applications (2nd ed.)*. Academic Press [Chapter 4 for MD](https://www.eng.uc.edu/~beaucag/Classes/AdvancedMaterialsThermodynamics/Books/%5BComputational%20science%20(San%20Diego,%20Calif.)%5D%20Daan%20Frenkel_%20Berend%20Smit%20-%20Understanding%20molecular%20simulation%20_%20from%20algorithms%20to%20applications%20(2002,%20Academic%20Press%20)%20-%20libgen.lc.pdf)

3. Listyarini, R.V., Kriesche, B.M., and Hofer, T.S., *Journal of Chemical Theory and Computation* 2024 20 (8), 3028-3045 DOI: [10.1021/acs.jctc.4c00162](https://pubs.acs.org/doi/full/10.1021/acs.jctc.4c00162)