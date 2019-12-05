# HPLSetup
Bash script to customize the [HPL](https://www.netlib.org/benchmark/hpl/) input file (HPL.dat) for a given number of cores and amount of memory. Many people use a website like [this one from Advanced Clustering](https://www.advancedclustering.com/act_kb/tune-hpl-dat-file/) to customize HPL.dat; this script does something similar but at the command line so that testing different parameters can be automated.

Usage is:
```
$ ./hpl_setup.sh -u
Script to set N, NB, P, and Q in HPL.dat given a number of cores and target percent memory
usage: hpl_setup.sh [-np procs] [-pm % memory to use] [-m gb/core] [-nb blocksize] [-n hpl n parameter] [-p hpl p parameter] [-q hpl q parameter]
  -np     number of processors (default: use SLURM_NTASKS or PBS_NP)
  -pm     percent memory to use (default: 85, roughly maximum performance)
  -m      system memory per core in GB (default: 4)
  -nb     HPL block size (NB parameter) (default: 160)
  -n      HPL problem size (N parameter) (default: compute to fit target percent memory)
  -p      HPL P parameter (PxQ = number of processes) (default: compute from number of processes np)
  -q      HPL Q parameter (PxQ = number of processes) (default: np/p)
 ```

For example, here we setup HPL.dat to run with 128 MPI processes using about 10 percent of memory (for relatively short runtime) on a system with 4 GB/core of memory:
```
$ ./hpl_setup.sh -np 128 -m 4 -pm 10
Block size (-nb) not provided. Using default value of 160.
HPL problem size (-n) not specified. Using calculated value of 82720 (4 gb/core, hplpctmem=10).
P parameter (-p) not specified. Using calculated value of 8.
Q parameter (-q) not specified. Using calculated value of 16.
Making the following changes to HPL.dat:
 N = 82720
NB = 160
 P = 8
 Q = 16
HPL setup complete.
```
