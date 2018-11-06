# HSCC2019_RE

This is the readme file of the HSCC2019 Repeatibility Evaluation (RE) package.
Instructions are provided for installing and running the benchmarks.

*Note.* `HSCC2019_RE.jl` is just a "wrapper" module for running the
benchmarks of this RE. The actual algorithms are implemented in the
package [Reachability.jl](https://github.com/JuliaReach/Reachability.jl).

## Introduction

The case study is the model *filtered oscillator* model. This is a model
parametric in the number of filters.

**Overview.** To install and run the benchmarks, the following three steps are
needed:

1. Download and install Julia in your machine using the official download links.
2. CLone this repository and run the script `install.sh`.
3. Run the script `run.sh` to execute the benchmarks and obtain results.

The results are saved in the file `results.md`.

Below we explain these three steps in some detail. A section on known issues is given
in the end. If you still have problems or questions, do open an issue in the issue
tracker of this repository, or directly contact us in our
[gitter channel](https://gitter.im/JuliaReach/Lobby) or via email.


## Installation

This package requires Julia v0.6.4 or later.
Refer to the [official documentation](https://julialang.org/downloads) on how to
install and run Julia in your system. 

Once you have installed Julia, you should be able to open it in a terminal (shell)
with the command `julia`, and see the welcome message similar to

```
$ julia
               _
   _       _ _(_)_     |  A fresh approach to technical computing
  (_)     | (_) (_)    |  Documentation: https://docs.julialang.org

   _ _   _| |_  __ _   |  Type "?help" for help.
  | | | | | | |/ _` |  |
  | | |_| | | | (_| |  |  Version 0.6.1 (2017-10-24 22:15 UTC)
 _/ |\__'_|_|_|\__'_|  |  Official http://julialang.org/ release
|__/                   |  x86_64-apple-darwin14.5.0

julia>
```

To install the reachability API we provide the shell script `install.sh` contained
in this folder. Execute the script `install.sh` with the command:

```
$ ./install.sh
```

*Note.* The script `install.sh` evaluates the following commands in your Julia installation:

```julia
julia> Pkg.clone("https://github.com/JuliaReach/Reachability.git")
julia> Pkg.clone("https://github.com/JuliaReach/HSCC2019_RE.git")
julia> Pkg.add("BenchmarkTools")
julia> Pkg.add("PkgBenchmark")
```
Since `Reachability.jl` has several dependencies and the other packages also
have their dependencies, this whole process will take between 5-20 minutes in a fresh
Julia installation.

## Running the benchmarks

To run and get the benchmark results in the file `results.md`, execute the
bash script `run.sh` with the command:

```
$ ./run.sh
```

The `results.md` file is saved in your current working directory.

*Note.* This script automatically executes the commands needed to launch the reachability computations,

```julia
julia> using PkgBenchmark, Reachability
julia> results = benchmarkpkg("HSCC2019_RE")
julia> export_markdown("results.md", results)
```
Each computation is performed several times, to reduce noise and obtain
statistically meaningful timings. The script can take several minutes.

In the results tables, the reported time is the minimum time in seconds for each safety property check.
Other statistics such as mean and max values can be found by looking at the entries
of the `results` structure. For more advanced settings we refer to the official
[BenchmarkTools](https://github.com/JuliaCI/BenchmarkTools.jl/blob/master/doc/manual.md) documentation.

## Known issues

1. To be able to run the shell script, you may have to give the appropriate permissions.
   In Linux and MacOS systems this is done with the command:

   ```
   $ chmod 744 run.sh
   ```

2. If running one of the shell scripts give failures, try running it a second time.
