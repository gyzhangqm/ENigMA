# ENigMA - Extended Numerical Multiphysics Analysis #

ENigMA is an object-oriented C++ template library which aim is to provide multi-physics simulation in a multi-domain environment. The code implements several numerical methods such as Finite Volume Methods (FVM), Finite Difference Methods (FDM), Finite Element Methods (FEM), Boundary Element Methods (BEM), Smoothed Particle Hydrodynamics (SPH), etc. for numerical approximation of Partial Differential Equations (PDE) in each domain. 

ENigMA provides classes for mesh generation (triangular, block, constrained tetrahedral, etc), intersection and clipping operations and implements R-tree, octree and hashgrid methods for spatial searching. It can be used for three-dimensional flow, thermal and structural analysis.

It was developed to be cross-platform using STL, Eigen (for vectors and matrices) and exprtk (for math expressions). The SWIG tool is used to expose ENigMA's classes and methods to other languages such as Python, C#, etc. It also uses Gtest for unit testing (> 160 unit tests), CMake is used for cross-platform building and Git is used for source code management.

![mesh](https://github.com/bjaraujo/ENigMA/blob/master/images/mesh.png)

ENigMA implements several operators such as divergence, laplacian, gradient, etc. so, for example, a heat equation such as: 

![equation](https://github.com/bjaraujo/ENigMA/blob/master/images/equation.gif)

can be represented in ENigMA as:

```cpp
CPdeEquation<double> aPdeEquation(1.0 / dt * ddt<double>(u) - alpha * laplacian<double>(u) = 0);
```

The argument passed to the CPdeEquation accepts an object of type CSleSystem which is a linear system of equations. The solution of the PDE is achieved by simply calling solve method:

```cpp
aPdeEquation.solve(u);
```

### Structure ###

ENigMA has the following namespaces:

- **analytical**: analytical solutions
- **geometry**: geometry, intersection, clipping, spatial search (R-tree, octree, hashgrid), etc.
- **integration**: numerical integration
- **bem**: Boundary Element Method (BEM)
- **fdm**: Finite Difference Method (FDM)
- **fem**: Finite Element Method (FEM)
- **fvm**: Finite Volume Method (FVM)
- **sph**: Smoothed Particle Hydrodynamics (SPH)
- **pde**: Partial Differential Equations
- **sle**: System of Linear Equations
- **mesh**: mesh generation (block, triangular, tetrahedral*, hexahedral, etc.)
- **post**: post-processing
- **stl**: STL file processing

Note: the constrained advancing-front tetrahedral mesher is part of ENigMA+. Will be added to ENigMA source code base when this project reaches 100 stars. 

### Dependencies ###

Core:
- Eigen: http://eigen.tuxfamily.org
- Exprtk: https://github.com/ArashPartow/exprtk or dependencies folder
- RTree: https://github.com/nushoin/RTree (slightly modified) or dependencies folder
- ViennaCL (optional): http://viennacl.sourceforge.net

Tests:
- Gtest (optional): https://github.com/google/googletest

Examples:
- Qt (optional): https://www.qt.io
- VTK (optional): http://www.vtk.org
- OpenGL/GLUT (optional): http://freeglut.sourceforge.net
- Gmsh (optional): http://gmsh.info/

### Install ###

Configure correctly the environment variables (EIGEN_DIR, EXPRTK_DIR, RTREE_DIR, etc.) and run [CMake](https://cmake.org).

- git clone https://github.com/bjaraujo/ENigMA.git
- cd ENigMA
- cmake-gui&
- setup source/build directory
- download Eigen and GTest
- set paths to Eigen, GTest, Exprtk  (dependencies folder), RTree (dependencies folder)
- configure/generate
- make

### Usage ###

- Check the tests and examples folders,
- Visit the [Wiki](https://github.com/bjaraujo/ENigMA/wiki),
- Run demo (releases).

### Quick Start ###

- Install python 3 64bit (if you don't have already), 
- Download the latest release (python wrapper),
- Create file named "Example1.py"
- Go to wiki and copy example "Creating a mesh using python"
- Run command "python Example1.py"

### Examples ###

#### A cylinder

![cylinder](https://github.com/bjaraujo/ENigMA/blob/master/images/occ_01.png) 
```python
from OCC.BRepPrimAPI import BRepPrimAPI_MakeCylinder

import ENigMAocc
        
cylinder = BRepPrimAPI_MakeCylinder(3.0, 10.0).Shape() 

mesh = ENigMAocc.meshShape(cylinder, 0.5, 1E-3)
ENigMAocc.saveMeshFile(mesh, "occ_01.msh")
```






