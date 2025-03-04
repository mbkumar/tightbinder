hBN 
=========================

The model for hexagonal boron nitride is a minimal one, based on :math:`p_z` orbitals exclusively with hoppings between first neighbours only [Galvani2016]_. The resulting band structure is the following:

.. image:: ../plots/hbn_bands.png
    :align: center

The configuration file for the model is:

.. code-block::
    :caption: examples/hBN.txt

    ! --------------------- Config file formatting rules ---------------------
    ! Lines starting with ! are comments
    ! Lines with # denote argument types and must be present (removing one or wirting it wrogn will result in error)
    ! Blank spaces are irrelevant
    ! All numbers must be separated by either spaces, commas or semicolons
    ! BEWARE: Leaving a blank space at the beginning of a line will result in it being skipped
    !
    ! This model is based on the paper "Excitons in Boron Nitride Single Layer"
    ! https://doi.org/10.1103/PhysRevB.94.125303
    ! --------------------- Material parameters ---------------------
    #System name
    Minimal hBN model

    #Dimensionality
    2

    #Bravais lattice
    ! Each row corresponds to one vector of the basis (vectors have to be in R^3).
    ! For 1D and 2D systems, the z (third) component must be zero (z should always be regarded as height component).
    2.16506 1.25 0.0
    2.16506 -1.25 0.0

    #Species
    ! Number of atomic species
    2

    #Motif
    ! Each row corresponds to one vector (atom) of the basis; fourth number denotes atomic species.
    ! Numbering of species starts at 0.
    0 0 0 0
    1.443376 0 0 1

    #Orbitals
    ! Always use cubic harmonic orbitals.
    ! Order is irrelevant.
    ! Possible orbitals are: s, px, py, pz, dxy, dyz, dzx, dx2-y2, d3z2-r2
    s
    s

    #Filling
    ! Specify number of electrons per chemical species; one line per species. 
    ! Fillings can be fractional, but total number of electons in unit cell must be an integer.
    0.5
    0.5

    #Onsite energy
    ! One for each different orbital defined above.
    ! In case of having several atomic species multiple line must be specified, one for each element.
    3.625
    -3.625

    #SK amplitudes
    ! Order is fixed: Vsss, Vsps, Vpps, Vppp, Vsds, Vpds, Vpdp, Vdds, Vddp, Vddd (separated by spaces).
    ! Not present amplitudes can be omitted but ordering has te be respected always.
    ! The syntax for SK amplitudes allows to specify between which species are the hoppings, as well as
    ! which is the corresponding neighbour. 
    ! Syntax is: [species1, species2; n-th neighbour] V1 V2 ...
    [0, 1] -2.3

    #Spin
    ! Determine whether the model is spinless (spin polarized) or spinful.
    ! Must be either True (spinful) or False (spinless); if left blank it will default to False.
    ! NOTE: True or False must be capitalized.
    False

    #Spin-orbit coupling
    ! Note: Using a non-zero value will automatically produce a spinful model.
    ! Amplitude must be specified for all species; one line per species.
    0

    ! --------------------- Simulation parameters ---------------------
    #Mesh
    ! Number of kpoints in each direction. Syntax is Nx Ny Nz
    ! It suffices to provide the required number of points depending on the system's dimension
    100 100

    #High symmetry points
    ! Label of points which define the path to evalute the bands of the system
    G K M G



.. [Galvani2016] Excitons in boron nitride single layer, Thomas Galvani, Fulvio Paleari, Henrique P. C. Miranda, Alejandro Molina-Sánchez, Ludger Wirtz, Sylvain Latil, Hakim Amara, and François Ducastelle, Phys. Rev. B 94, 125303 (2016), https://doi.org/10.1103/PhysRevB.94.125303