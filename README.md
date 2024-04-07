# CO_Au111
#Employ the model
With a trained model, users can employ the model to obtain the energies and atomic force vectors of configurations. Furthermore, the models can be interfaced into the MD package for atomic simulation.

Parameters trained for the neutral state PES, the anionic state PES and the coupling between the two states are in “/para-neutral”, “/para-anion” and “/para-coupling”, respectively. And you can change these paths in mod_*.f90. In each parameter dir, you can see “input”, “cell”, “atom”, “W_[element name]1” and “weight_wave_[element]”. “inputs” contains parameters used to train the neural network (NN) potential. “cell” contains the lattice parameter of the system. “atom” contains the atom names with the order of the input geometry. “W_[element name]1” and “weight_wave_[element]” contain parameters of the neural network structure.
#The Fortran interface:
At the beginning, users need to compile the Fortran files to obtain an executable file. Then users need to call the subroutine ‘init_pes’ to do some initializations. Then you can pass the coordinates of configurations by calling the subroutine. “EANN_out(table, start_force, coor, y, force)”

“table”: The form of the coordinates. “0”: Cartesian coordinates. “1”: Fraction coordinates.
“start_force”: “1”: energies and force vectors output with the variable ‘y’ and ‘force’ in the subroutine respectively; “0”: only energies obtained;
“coor”: the coordinates of the configurations provided for the calculating;
“y”: the array holding the energy of the corresponding configurations;
“force”: the array holding the atomic force of the corresponding configurations. Finally, you need to call “deallocate_all” to release the memory of program.
We also give an example to call energies and forces on the three PESs in “test.f90”. “h00”, “h11”, and “h01” are the neutral state energy (in eV), the anionic state energy (in eV) and the coupling strength between the two states (in eV). “force_neutral”, “force_anion”, “force_coupling” are the corresponding forces (in eV/Å).
