This document contains some information about how to use *Maxent.py* to do analytical continuation to imaginary-frequency Green's function data. We use **Maximum Entropy Method(MEM)** based on the paper: **M. Jarrell and J.E. Gubernatis, Phys. Rep. 269 (1996) 133**. 

# Requirement:
------------
python installed (better ipython IDE)

matplotlib, scipy and numpy installed.

# Instruction:
------------
In terminal, run *Maxent.py* as:
> python Maxent.py test.dat

or in ipython IDE,
> %run Maxent.py test.dat

where *test.dat* is file that contains data. Here is format that required by *test.dat*: The first column is real frequency, the second column is the real part of Green's function, the third column is the imaginary part of the Green's function and so forth. The seond and thid column is the first set of Green's function data. And the forth and fifth column is the second set of Green's function data. Please see the *./test/test1/test1.dat* file as a reference.

e.g.

| w   |  G1.real|   G1.imag |  G2.real |   G2.imag     | ... |
|-----|---------|-----------|--------- |--------       | --- |
| 0.1 |    111  |     112   |    121   |    122        | ... |
| 0.2 |   211   |    212    |    221   |     222       | ... |
| ... | ...     |    ...    |    ...   |       ...     | ... |
	


After finishing running the code, it will generate the MaxEnt result graph and some files to store the data. *test.dat.p* is pickle file that stores dictionary data. *test.datComparison.paf* is the Maxent graph. *test.datmaxent.dat* stores the Maxent dat. The first column in it is real frequency and the second column is the spectral function A(w). *test.datPalpha.dat* has the posterior probability distribution of P(alpha|G). The first column is the alpha and the second column is P(alpha|G). These files are enough for publishing purpose.

There is also a *Draw.py* file to plot. Run
> python Draw.py test.dat.p

will create two graphs. One is MEM result and inset is the posterior probability distribution. Another graph is the trend how spectral function evolves with regularization paramter alpha.

# Change Parameter:
-----------------
For different cases, the parameter used in the Maxent.py file should be changed. In the file, Maxent class has several arguments as input.

	filename: the file that stores imaginary-frenquency Green's function data
	column: number of column in the file, an odd number.
	numRfre: the number of grid for spectral function A(w).
	wmin: minimum real frequency
	wmax: maximun real frequency
	defaultModel: this parameter can be 'gaussian', 'straightline' or 'input'.
	tol: tolerance for minimization. 1e-12 for SLSQP; 1e-5 for Bryan
	std: whether or not use the standard deviation.
	alphamin: value of minimun alpha in log space.
	alphamax: value of maximum alpha in log space
	numAlpha: number of alphas.
	minimizer: "SLSQP" or "Bryan".


