Hydrogen chain
=========================
One of the simplest models to check that the code is working properly. We consider a linear chain of atoms with :math:`s` orbitals only. Do note that the SK amplitude used for these s orbitals does not actually correspond
to any hydrogen calculation. The band structure can be obtained analitically in this case:

.. math::

    \varepsilon(k) = \varepsilon_0 - 2t\cos{ka}

where :math:`\varepsilon_0` is the onsite energy, and :math:`t` the hopping amplitude (amplitude for :math:`s` orbital in the SK context).
The band structure as obtained with the configuration file is:

.. image:: ../plots/chain_bands.png
    :align: center

Note that we need to include spin in the model to achieve half-filling; if we were to consider only one orbital (spinless) then the resulting system would have to be either empty of full, since the number of electrons
per unit cell must be an integer. The configuration file is:

.. code-block::
    :caption: examples/chain.txt

    ! --------------------- Config file formatting rules ---------------------
    ! Lines starting with ! are comments
    ! Lines with # denote argument types and must be present (removing one or wirting it wrogn will result in error)
    ! Blank spaces are irrelevant
    ! All numbers must be separated by either spaces, commas or semicolons
    ! Beware: Leaving a blank space at the beginning of a line will result in it being skipped
    ! -------------------------- Material parameters -------------------------
    #System name
    Test chain

    #Dimensionality
    1

    #Bravais lattice
    ! Each row corresponds to one vector of the basis (vectors have to be in R^3)
    ! For 1D and 2D systems, the z (third) component must be zero (z should always be regarded as height component)
    1 0 0

    #Species
    ! Number of atomic species (isoelectronic at the moment)
    1

    #Motif
    ! Each row corresponds to one vector of the basis; fourth number denotes atomic species
    ! Numbering of species starts at 0.
    0 0 0 0

    #Orbitals
    ! Always use cubic harmonic orbitals
    ! Order is irrelevant
    ! Possible orbitals are: s, px, py, pz, dxy, dyz, dzx, dx2-y2, d3z2-r2
    s

    #Filling
    ! Specify number of electrons per chemical species; one line per species. 
    ! Fillings can be fractional, but total number of electons in unit cell must be an integer.
    1

    #Onsite energy
    ! One for each different orbital defined above.
    ! In case of having several atomic species multiple line must be specified, one for each element.
    1

    #SK amplitudes
    ! Order is fixed: Vsss, Vsps, Vpps, Vppp, Vsds, Vpds, Vpdp, Vdds, Vddp, Vddd (separated by spaces).
    ! Not present amplitudes can be omitted but ordering has te be respected always.
    ! The syntax for SK amplitudes allows to specify between which species are the hoppings, as well as
    ! which is the corresponding neighbour. 
    ! Syntax is: [species1, species2; n-th neighbour] V1 V2 ...
    -0.3

    #Spin
    ! Determine whether the model is spinless (spin polarized) or spinful.
    ! Must be either True (spinful) or False (spinless); if left blank it will default to False.
    ! NOTE: True or False must be capitalized.
    True

    #Spin-orbit coupling
    ! Note: Using a non-zero value will automatically produce a spinful model.
    ! Amplitude must be specified for all species; one line per species.
    0

    ! --------------------- Simulation parameters ---------------------
    #Mesh
    ! Number of kpoints in each direction. Syntax is Nx Ny Nz
    ! It suffices to provide the required number of points depending on the system's dimension
    100

    #High symmetry points
    ! Label of points which make the path to evalute the bands of the system.
    K G K

