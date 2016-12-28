# Cellular Solids Notes

Daniel Cellucci - January 2016 (and onward)

My thesis defense is in May. Paper #3 of my thesis will be the culmination of work I've done on alternative approaches to the design and construction of digital cellular solids. This repository is a set of notes, code, and media describing that work and where I think it fits. My understanding is, at best, incomplete, so that is why I am sending this to you, dear reader, for feedback and thoughts.

## Introduction

Cellular solids are a class of materials composed of an interconnected network of struts and plates, which form the edges and faces of cells that tesselate three-dimensional space. The geometry of these cells can be represented by the constituent polyhedra in a convex uniform honeycomb. There are 28 such hon-eycombs, and common examples of the frameworks derived from these honeycombs include the Kelvin lattice, the Octet lattice, and the CubOctahedral lattice.

Cellular solids are found in many forms in nature, and have been applied in many engineering problems, including the construction of ultralight structural materials. Recent work in digital cellular solids introduced a decomposition of the cuboctahedral lattice into a single, two-dimensional part, which was then reversibly assembled into structures with, at the time, unprecedented stiffness-for-weight. This work showcased many desirable traits to the scalable assembly of cellular solids, including centimeter-scale construction, repairability, and mass-production of parts from high-performance materials. Subsequent work has demonstrated further capabilities of this approach, including robotic traversal and meter-scale
structures using a three-part strut-node construction.

## Background

The choice of polyhedral honeycombs is largely a historical one. The first cellular solids were stochastic foams formed by dissolving gas into a polymer, allowing the gas to nucleate into bubbles whose arrangement can be modelled by Plateau's laws. Polyhedral honeycombs like the Kelvin lattice (or tridecahedral lattice) are one such proposed solution to the laws, by partitioning space into identical elements which maximize the volume while minimizing the surface area (subsequent, "better" partitions have been found but they're irregular and only marginally better). When combined with Maxwell's rigidity criterion, polyhedral honeycombs are used to model the mechanical properties of these stochastic foams, by examining whether a lattice has sufficient coordination (struts meeting at a node) in order to be kinematically determined. Since the Kelvin lattice is not kinematically determined, its mechanical performance (in terms of specific stiffness) is suboptimal compared to other honeycombs, such as the Octet truss (tetrahedral-octahedral honeycomb).

With the rise of additive manufacturing, the 'map' for cellular solids became the 'territory', and researchers started examining the performance of these kinematically determined honeycombs. The results agreed with what was expected with the rigidity criterion- a kinematically determined lattice displayed superior mechanical response to one that wasn't. 

### Manufacturing Concerns

While the complexity of the octet truss is not a real concern when made using additive manufacturing, the high coordination of the lattice makes decomposition into easily-manufactured building block parts a non-trivial task. By "easily manufactured" I mean

1. the primary structural part can use an existing 2.5D process, such as casting, stamping, abrasive waterjet cutting. 
2. the part is finite, as in it does not span the full size of the structure, so the parts can be tightly packed before assembly
3. the number of parts is minimized (ideally one or two)

To date, no one I know of has successfully decomposed the octet truss into a set of peices which satisfy these criteria. It might just be a design problem, but another solution is to examine alternative methods for deriving frameworks whose decompositions satisfy these criteria from the outset.

##### Objective: A Better Definition of What "Easily Manufactured" Means

Being able to provide clear, quantitative measures for how the above criteria translate to substantively better results than other methods. Possible avenues include:

1. Measuring the embodied energy of various processes e.g. injection molding and assembly vs. 3d printing and plating. 
2. Packing ratios for flat parts versus voxel parts
3. Perhaps mass scaling for 2.5D nodes versus 3d?

### TPMS-Derived Frameworks

You can read more about them in the attached paper, but essentially TPMSes are three-dimensional, Riemannian manifolds which belong to a space group. Because of this, all straight lines which are embedded on a TPMS will meet at a point which is locally flat, and a solution which spans a single unit cell is sufficient to solve for the entire lattice. 

While the 2D node makes the decomposition of the lattice into "easily manufactured" building blocks, finding the embedded straight lines is a non-trivial task. Right now there are two methods: finding the minimal patch and brute-force searching the space for straight line intersections. 

#### Method 1: Minimal Patches

The minimal patch of a TPMS is a simply connected piece of minimal surface. If the edges of the patch form a spherical polygon whose angles are of the form Pi/k, then the minimal surface can be extended by 180-degree-rotation about the boundary edges to form a complete, immersed minimal surface. As a result, the edges of the patch are the embedded straight lines of the TPMS. Additionally, there are no straight lines in the patch, since these lines would form axes for further simplification of the surface. 

Finding these minimal patches is decidedly nontrivial. Karcher [cite], describes using the conjugate surface method. The process involves starting with the conjugate TPMS' asymmetric unit (which is decided by the space group this conjugate surface occupies) to construct the polygon of the conjugate surface method by utilizing the relationship between the asymmetric unit and the minimal patch. This process is limited to only very simple TPMS- those whose minimal contours can be 

#### Method 2: Brute-Force



##### Questions about Finding embedded straight lines 

1. Are there alternative approaches that can guarantee existence?

## Performance Analysis

In a paper I submitted to ASME MSEC, I used the two methods above to "find" (verify) two lattices, one derived from the D-Schwarz and one derived from the P-Schwarz TPMS. I then tested these two lattices using two methods for assessing the rigidity of a periodic framework: the symmetry-extended counting rules described by Guest and Fowler and the multiscale linear analysis of Vigliotti and Pasini. 

### Symmetry Extended Counting Rules

Guest and Fowler introduced a method for examining the mobility of a framework by considering the symmetries of that framework. This extensions are written in the form of reducible representations of characteristics objects of the framework, which collect the characters of these objects over the symmetry operations which constitute the framework's space group. The general equation for these structures is then:
$$
\Gamma(m) - \Gamma(s) = \Gamma(j) \times \Gamma_T - \Gamma(b) + \Gamma_T \times \Gamma_T - \Gamma_T - \Gamma_R
$$
Where *m* is the number of mechanism states, *s* is the number of states of self-stress, *j* is the number of joints, *b* is the number of bars, and *T* and *R* are the relevant rigid-body translations and rotations, respectively. 

#### D-Schwarz 

D-Schwarz belongs to the space group F-43m, or Td. The character table of Td is:

|   Td |  E   | 8C3  | 3C2  | 6S4  | 6sd  |
| ---: | :--: | :--: | :--: | :--: | :--: |
|   A1 |  1   |  1   |  1   |  1   |  1   |
|   A2 |  1   |  1   |  1   |  -1  |  -1  |
|    E |  2   |  -1  |  2   |  0   |  0   |
|   T1 |  3   |  0   |  -1  |  1   |  -1  |
|   T2 |  3   |  0   |  -1  |  -1  |  1   |

Applying the symmetry extended counting rules to D-Schwarz produces

|   Td   |  E   | 8C3  | 3C2  | 6S4  | 6sd  |                |
| :----: | :--: | :--: | :--: | :--: | :--: | :------------- |
|  R(j)  |  4   |  1   |  0   |  0   |  2   |                |
| xR(t)  |  3   |  0   |  -1  |  -1  |  1   |                |
|   =    |  12  |  0   |  0   |  0   |  2   |                |
| -R(b)  | -12  |  0   |  -4  |  0   |  2   |                |
|   =    |  0   |  0   |  -4  |  0   |  2   | = -A2-E-T2     |
| R(t)^2 |  9   |  0   |  1   |  1   |  1   | = A1+E+T1+T2   |
| -R(t)  |  -3  |  0   |  1   |  1   |  -1  |                |
| -R(r)  |  -3  |  0   |  1   |  -1  |  1   |                |
| Rm-Rs  |  3   |  0   |  -1  |  1   |  3   | = A1 - A2 + T2 |

What's important about this table is the last line- according to the counting rules, there are two mechanism states with symmetries A1 and T2, and a state of self-stress with symmetry A2. Furthermore, the mechanism state A1 has the full symmetry of the lattice. That is, there is no way the lattice can be kinematically determined if it is comprised of only pin-joints. 

### Multiscale Linear Analysis

While the above gives us a sense for what general behavior we expect, in order to get specific macroscopic properties from the lattice we need to look to the multiscale linear analysis provided by Vigliotti and Pasini. The primary product of this analysis is a stiffness matrix **K** which allows the determination of the effective modulus in the three principle directions of the lattice as well as the shear and hydrostatic response. 

Vigliotti and Pasini's paper describes the process for generating this matrix from the lattice primitive cell.

