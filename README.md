# Patches and Singularity Recipe files for building the UC2 container
This repo contains work related to containerising software components of PROCESS use case 2 (UC#2), essentially composed of Singularity recipe files and patches for fixing issues or adding features into those components.

## Patches
**remotecommand.patch** is a patch to the eponym file in the LOFAR genericpipeline.py which allows to run some tasks from the container in a distributed fashio using SSH

## Singularity recipe files
There are three groups of recipe files:
* The first group contains **lofarbase.def**, **lofar.def**, **factor.def** and **uc2-factor.def**. In order to build the UC2 Singularity container, they need to used successuvely in this order, each step using the output of the previous step. First, **lofarbase.def** is used to generate a container image **base.sif** via the command _sudo singularity build lbase.sif lofarbase.def_. Then, **lofar.def** is used to generate a container image **lofar.sif** via the command _sudo singularity build lofar.sif lofar.def_. etc.
* The second group is composed of only **uc2.def** which performs all the work achieved by above files in one go using the _sudo singularity build uc2.sif uc2.def_.
* The last group is composed of **ddf3t.def** and **lofar-2.def**. The former uses the container image built from the latter to construct a UC2 container image with DDF as direction-dependent calibration software, instead of FACTOR.
