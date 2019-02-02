# HSCC2019_RE

This is the HSCC2019 Repeatability Evaluation (RE) package for the paper
*JuliaReach: a Toolbox for Set-Based Reachability*.

*Note.* This package is just a "wrapper" module for running the benchmarks.
The actual algorithms are implemented in the package
[LazySets.jl](https://github.com/JuliaReach/LazySets.jl) and
[Reachability.jl](https://github.com/JuliaReach/Reachability.jl).

## Introduction

We provide the code to

1. reproduce the figures and
2. run the experiments for the *filtered oscillator* model.

**Overview.** To install and run the benchmarks, the following steps are needed:

1. Install Julia (at least v0.6.4; the instructions below assume Julia v1.0.2).
2. Install the required Julia packages.
3. Clone this repository.
4. (optional) Install `SpaceEx`.

Below we explain these three steps in some detail.
If you have problems or questions, just open an issue in the issue tracker of
this repository, or directly contact us in our
[gitter channel](https://gitter.im/JuliaReach/Lobby) or via e-mail.


## Installation

Refer to the [official documentation](https://julialang.org/downloads) on how to
install and run Julia on your system. 

Once you have installed Julia, you should be able to open the REPL in a terminal
with the command `julia`.

Next you need to install the some packages.
Installation is run from the package mode in the REPL, entered by typing `]`.

```julia
pkg> add PACKAGE_NAME
```

Install the following packages in this way.

```
HybridSystems
MathematicalSystems
LazySets
Polyhedra
Optim
Plots
LaTeXStrings
GR
Random
```

You also need the `Reachability` package.
At the time of writing, this package is not published in Julia's package system,
so you need to clone the repository manually.
The following command fixes a version with known compatibility.

```julia
pkg> add https://github.com/JuliaReach/Reachability.jl#6340067f382bb0547a1ad45ddefcdab2053a3bcb
```

Finally, for cloning this repository, again use the `add` command.

```julia
pkg> add https://github.com/JuliaReach/HSCC2019_RE.git
```

Now exit the package mode by pressing the `backspace` key.

When the packages are used the first time, they are pre-compiled, which may take
a while.

The REPL is terminated by executing the following command.

```julia
julia> exit()
```

## Running the benchmarks

#### JuliaReach

To run the `JuliaReach` experiments, go to the folder of the same name and run
the following scripts in Julia.

```
create_figure_1.jl
create_figure_2.jl
create_figure_3.jl
create_figure_5.jl
create_table_1.jl
```

For instance, for running `create_figure_1.jl` from the REPL, type

```julia
julia> include("create_figure_1.jl")
```

#### SpaceEx

To run the `SpaceEx` experiments, install `SpaceEx` (get it from the 
[official web page](http://spaceex.imag.fr/) and add it to your `PATH`) and then
run the script `runsxmodels.sh` in the `SpaceEx` folder.
