# Homework Assignment 15

![Assignment 15](https://github.com/PGE383-HPC/assignment15/actions/workflows/main.yml/badge.svg)

In [Homework Assignment 9](https://github.com/PGE383-HPC/assignment9) we wrote a program that would process a data file, converting the raw data to true stress and strain, and compute the toughness,  and then in [Homework Assignment 13](https://github.com/PGE383-HPC/assignment13) we extended that code to make it parallel with [MPI.jl](https://juliaparallel.org/MPI.jl/latest/).  In this assignment, we will create another parallel solution this time using [DistributedArrays.jl](https://github.com/JuliaParallel/DistributedArrays.jl).

Your assignment is to complete the Julia module [assignment15.jl](src/assignment15.jl).  Specifically, you must complete the function `partition_data(strain::AbstractArray, stress::AbstractArray)`. 

In `partition_data()`, the `strain`/`stress` arguments are `Array`s that contain the entire stress and strain data only on the processor running the Julia REPL.  This function should distribute the `strain`/`stress` data to all processors available by turning them into `DistributedArrays`.  If done correctly, the code shouldn't need anymore modifications.

When the script is executed with the following command in the Terminal application from the root of the assignment repository

```bash
julia --project=. -e 'using Distributed; addprocs(3, exeflags="--project"); using assignment15; compute_toughness_parallel("./data/data.csv")'
```

it run on `3` processors and will print the toughness value to the screen. Your code should be parallel consistent, i.e. it should produce the exact same answer independent of the number of processors you specify.


## Testing

To see if your answer is correct, run the following command at the Terminal
command line from the repository's root directory

```bash
julia --project=. -e "using Pkg; Pkg.test()"
```

the tests will run and report if passing or failing.
