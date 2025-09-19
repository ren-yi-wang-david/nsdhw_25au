FTST

Basic Information
=================
FDM Thermal Simulator Tool
GitHub repository: https://github.com/ren-yi-wang-david/Thermal_Simulator_for_nsd
Problem to Solve
================
power induced thermal distribution,steady state heat transfer,etc.
Prospective Users
=================
this tool is developed for CAE,VLSI,CFD simulation user providing verification ,early stage prediction,thermal-aware co optimization.
System Architecture
===================
using FDM to discretize the governing equation of heat transfer 
using  LU decomposition for solver
using python for visualization
Using C++ to implement the algorithm.
Using pybind11 to wrap c++ in python.
Using pybind11 to make API in python.
C++: kernel system
Python: user interface
an user-friendly UI
wrap the kernel system by using pybind11
workflow:
===============
Input: Massive matrices(.txt) for power map 
Output:temperature distribution(.txt)and visualization output(heatmap)

API Description
===============
(python)
from FTST import ThermalSolver

solver = ThermalSolver(nx=50, ny=50, k=150.0)
solver.set_boundary("left", 300)
solver.set_boundary("right", 350)
solver.set_power_map("power_map.txt")

solver.run("LU")
solver.plot("heatmap.png")
solver.write_csv("temperature.txt")

Engineering Infrastructure
==========================
license:MIT
Testing framework: Google Test (C++), pytest (Python)
Compiler: g++, python
Build System: make
Version Control: git
Automatic build system: GNU make
Documentation: README.md
Programming languages: Python (visualization), C++ (computation)
golden:ansys icepak
Schedule
========
* Planning phase (6 weeks from 10/20 to 12/8):
* Week 1 (10/20): Initialize repository and Make/CMake build system; set up project structure;study heat transfer modeling.
* Week 2 (10/27): Implement 2D FDM discretization for steady-state heat equation; add Dirichlet boundary condition support; create Google Test cases.
* Week 3 (11/3): Implement LU decomposition solver in C++; validate with small synthetic power maps;and use icepak as golden function to check validation.
* Week 4 (11/10): Expose solver to Python using pybind11; enable NumPy array interop; test Python API with simple cases.
* Week 5 (11/17): Validate re-check results against Icepak golden function; run micro-benchmarks; finalize testing framework (Google Test + pytest)
* Week 6 (11/24): performance analysis and optimize:time,memory and error,etc.
* Week 7 (12/1):Improve documentation (README, tutorials, API reference); freeze v0.1 API; polish and release v0.1.0 with demo presentation.
* Week 8 (12/8): Prepare Final Report
References
==========
HeatandMassTransfer7thEdition-Incropera-dewitt

