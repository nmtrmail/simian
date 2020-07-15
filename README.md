# Simian JIT PDES

=================================================================================

### Simian Just In Time Compiled Process Oriented Conservative Parallel Discrete Event Simulator from LANL
=================================================================================

Nandakishore Santhi (nsanthi at lanl dot gov)

Simian is a JIT compiled Process and Event Oriented Parallel Discrete Event Simulator with implementations in Lua(jit), Python(PyPy) and Javascript.
Simian has both a conservative (default) and an optimistic (experimental, old version was released in public repo https://github.com/annonch/simian. A newer optimistic mode is currently under development) execution mode.
Simian rivals other leading PDES engines written in compiled languages in terms of both the event-rate speed as well as the strength of its simple, yet powerful features.

SimianLua contains the Lua implementation and it needs luajit-2.1.
SimianPie contains the Python implementation, which needs Python 2.7.x with greenlets (optional) or Pypy 2.4.x. MPICH 3.1.4 or OpenMPI 1.6.x are optionally needed if using MPI.
SimianJS contains the Javascript implementation.

In general the execution speeds are in the following order for various language implementations (Fastest to Slowest):

    SimianLua with Luajit-2.1
    SimianJS with included modified MasalaChai interpreter
    Other leading PDES simulators in C++ or C
    SimianLua with Lua-5.1
    SimianPie with PyPy-2.x
    SimianPie with CPython-3.x
    SimianPie with PyPy-3.x
    SimianPie with CPython-2.x
    ...

See Docs for API documentation (Somewhat dated, but still useable. Will be updated soon!).
SimianLua/Examples has examples of SimianLua usage.
SimianPie/Examples has examples of SimianPie usage.
SimianJS/Examples has examples of SimianJS usage.
Below examples for SimianLua usage, but SimianPie and SimianJS usage are similar.

## If not using MPI:
    Set useMPI flag to false when initializing the Simian PDES Engine

## To use MPI with Simian (Lua):

### If using MPICH:
    (tested with 3.1.3)
    Set useMPI flag to true. Set a link to libmpich.[dylib/so/dll] in the top directory

### If using OpenMPI:
    (some later versions such as 1.8.3 have a serious bug in message size reporting; use 1.6.x)
    Set useMPI flag to true. Set a link to libmpi.[dylib/so/dll] in the top directory, and then comment within file Simian/MPI.lua line 'require "MPICH"' and uncomment in file Simian/MPI.lua line 'require "MPI"'

## To use the Python version SimianPie:
    SimianPie is tested to work with CPython 2.7.x, PyPy-v7.3.1, Python-3.7, and PyPy3.6-v7.3.1
    When using SimianPie along with MPI, SimianPie works with MPICH2 using CTypes - if only OpenMPI is available use SimianLua or if Python version is unavoidable, then user should write a CTypes wrapper for OpenMPI similar to the distributed CTyped wrapper for MPICH 3.1.3
        Set useMPI flag to true. Set a link to libmpich.[dylib/so/dll] in the top directory or pass absolute path to the library to Simian() when creating the engine.

## Test with pHold app without MPI:
    cd SimianLua; luajit Examples/phold-noop-noMPI.lua

## Testing with MPI on LANL PDES benchmark app:
    (on a medium sized cluster with more than 1000 cores)
    cd SimianLua; mpirun -np 1000 luajit-2.1.0-alpha Examples/pdes_lanl_benchmarkV8.lua 1000 100 1 0 0 false 1 0 100000 0 0.5 1 10 1000 1 true LANL_PDES.log

## LANL internal reference:
CODE Title: Simian, version 1.65 (OSS)

LACC #:  LA-CC-15-015

Copyright Number Assigned: C15036

Funding source: Laboratory-Directed Research and Development (LDRD)
