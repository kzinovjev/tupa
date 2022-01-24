[![Twitter Follow](https://img.shields.io/twitter/follow/mdpoleto?style=social)](https://twitter.com/mdpoleto)

# **TUPÃ**: Electric field analyses for molecular simulations

![alt text](https://github.com/mdpoleto/tupa/blob/main/LOGO/TUPÃ_LOGO.png "TUPÃ")

## What is TUPÃ?
**TUPÃ** (pronounced as *too-pun* / *to͞o-pən*) is a python algorithm that employs MDAnalysis engine to calculate electric fields at any point inside
the simulation box throughout MD trajectories. **TUPÃ** also includes a PyMOL plugin to visualize electric
field vectors together with molecules.

Required packages:

* MDAnalysis >= 1.0.0
* Python     >= 3.x
* Numpy      >= 1.2.x

------------------------------
## Installation instructions

First, make sure you have all required packages installed. For MDAnalysis installation procedures, [click here](https://www.mdanalysis.org/pages/installation_quick_start/).

After, just clone this repository into a folder of your choice:

    git clone https://github.com/mdpoleto/tupa.git

To use **TUPÃ** easily, copy the directory pathway to **TUPÃ** folder and include an alias in your ~/.bashrc:

    alias tupa="python /path/to/the/cloned/repository/TUPA.py"

To install the PyMOL plugin, open PyMOL > Plugin Manager and click on "Install New Plugin" tab.
Load the **TUPÃ** plugin and use it via command-line within PyMOL. To usage instructions, read our FAQ.


## TUPÃ Usage
**TUPÃ** calculations are based on parameters that are provided via a configuration file,
which can be obtained via the command:

    tupa -template config.conf


The configuration file usually contains:

    [Environment Selection]
    sele_environment      = (string)             [default: None]

    [Probe Selection]
    mode                = (string)             [default: None]
    selatom             = (string)             [default: None]
    selbond1            = (string)             [default: None]
    selbond2            = (string)             [default: None]
    targetcoordinate    = [float,float,float]  [default: None]
    remove_self         = (True/False)         [default: False]
    remove_cutoff       = (float)              [default: 1 A ]

    [Solvent]
    include_solvent     = (True/False)         [default: False]
    solvent_cutoff      = (float)              [default: 10 A]
    solvent_selection   = (string)             [default: None]

    [Time]
    begintime           = (integer)            [default: 0]
    endtime             = (integer)            [default: None]
    dt                  = (integer)            [default: 1]


A complete explanation of each option in the configuration file is available via the command:

    tupa -h

**TUPÃ** has 3 calculations MODES:

* In **ATOM** mode, the coordinate of one atom will be tracked throughout the trajectory to serve as target point.
If more than 1 atom is provided in the selection, the center of geometry (COG) is used as target position. An example
is provided HERE.

* In **BOND** mode, the midpoint between 2 atoms will be tracked throughout the trajectory to serve as target
point. In this mode, the bond axis is used to calculate electric field alignment. By default, the bond axis is
define as *selbond1 ---> selbond2*. An example is provided HERE.

* In **COORDINATE** mode, a list of [X,Y,Z] coordinates will serve as target point in all trajectory frames.
An example is provided HERE.

***IMPORTANT***:
* All selections must be compatible with MDAnalysis syntax.
* **TUPÃ does not handle PBC images yet!** Trajectories MUST be re-imaged before running TUPÃ.
* **Solvent** molecules in PBC images are selected if within the cutoff. This is achieved by applying the *around* selection feature in MDAnalysis.
* **TUPÃ does not account for Particle Mesh Ewald (PME) electrostatic contributions!** To minimize such effects, center your target as well as possible.
* If using COORDINATE mode, make sure your trajectory has no translations and rotations. Our code does not account for rotations and translations.


## TUPÃ PyMOL Plugin (pyTUPÃ)

To install *pyTUPÃ* plugin in PyMOL, click on Plugin > Plugin Manager and then "Install New Plugin" tab.
Choose the *pyTUPÃ.py* file and click Install.

Our plugin has 3 functions that can be called via command line within PyMOL:

* **efield_point**: create a vector at a given atom or set of coordinates.
```
efield_point segid LIG and name O1, efield=[-117.9143, 150.3252, 86.5553], scale=0.01, color="red", name="efield_OG"
```

* **efield_bond**: create a vector midway between 2 selected atoms.
```
efield_point resname LIG and name O1, resname LIG and name C1, efield=[-94.2675, -9.6722, 58.2067], scale=0.01, color="blue", name="efield_OG-C1"
```

* **draw_bond_axis**: create a vector representing the axis between 2 atoms.
```
draw_bond_axis resname LIG and name O1, resname LIG and name C1, gap=0.5, color="gray60", name="axis_OG-C1"
```

--------------------------
## Citing TUPÃ

If you use **TUPÃ** in a scientific publication, we would appreciate citations to the following paper:

Marcelo D. Polêto, Justin A. Lemkul. *TUPÃ: Electric field analysis for molecular simulations*, 2022.

Bibtex entry:
```
@article{TUPÃ2022,
    author = {Pol\^{e}to, M D and Lemkul, J A},
    title = "{TUPÃ : Electric field analyses for molecular simulations}",
    journal = {},
    year = {},
    month = {},
    issn = {},
    doi = {},
    url = {},
    note = {},
    eprint = {},
}
```


## Contact information
E-mail: mdpoleto@vt.edu / jalemkul@vt.edu
