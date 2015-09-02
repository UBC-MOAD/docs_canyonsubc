***************************
Building and Running MITgcm
***************************

Working on :kbd:`orcinus`
=========================

This section describes the steps to set up and run the MITgcm code for the UBC EOAS Canyons group configurations on the `orcinus.westgrid.ca`_ HPC cluster.

.. _orcinus.westgrid.ca: https://www.westgrid.ca/orcinus

When working on the Westgrid clusters the :command:`module` command must be used to load extra software components.
The required modules vary from cluster to cluster.
On :kbd:`orcinus` load the :kbd:`python` module with:

.. code-block:: bash

    $ module load python

to make Python 2.7,
the python-netCDF4 package,
and Mercurial available to you.


Create a Workspace and Get the Repos
------------------------------------

.. code-block:: bash

    $ mkdir -p $HOME/canyons
    $ cd $HOME/canyons

Use the CVS version control tool to do a checkout of the latest MITgcm source code.
Use the password :kbd:`cvsanon` when the :command:`cvs login` command prompts you for a password:

.. code-block:: bash

    $ export CVSROOT=':pserver:cvsanon@mitgcm.org:/u/gcmpack'
    $ cvs login
    $ cvs co -P MITgcm

Use the Mercurial version control tool to clone the `CanyonsUBC optfiles`_ repo from Bitbucket:

.. _CanyonsUBC optfiles: https://bitbucket.org/canyonsubc/optfiles

.. code-block:: bash

    $ hg clone ssh://hg@bitbucket.org/canyonsubc/optfiles


Building the Code
-----------------

The MITgcm docs describe several ways of `building the code`_.
Here,
we will do the build in a directory outside of the :file:`MITgcm` and :file:`optfiles` directory trees.

.. _building the code: http://mitgcm.org/public/r2_manual/latest/online_documents/node94.html

.. note::

    For the purposes of developing the build instructions for :kbd:`orcinus` the :file:`MITgcm/verification/rotating_tank/` configuration is used,
    but the steps below should be adaptable to your research configuration(s).

Create a configuration build directory:

.. code-block:: bash

    $ cd $HOME/canyons
    $ mkdir -p rotating_tank/build
    $ cd rotating_tank/build

Build the code:

  .. code-block:: bash

      $ $HOME/canyons/MITgcm/tools/genmake2 \
          -rootdir=$HOME/canyons/MITgcm \
          -mods=$HOME/canyons/MITgcm/verification/rotating_tank/code
          -of=$HOME/canyons/optfiles/orcinus_mpi.opt \
          -mpi
      $ module load intel
      $ module load intel/14.0/netcdf_hdf5
      $ make depend
      $ make

The :command:`module load` commands bring
the Intel OpenMPI Fortran compiler,
and its netcdf and hdf5 libraries into your environment for the :command:`make` steps.
Those modules are also required to run the code,
so you need to include those :command:`module load` commands in your PBC script.
However,
due to some weirdness in the :kbd:`orcinus` modules setup,
they *must not* be loaded when you run :command:`MITgcm/tools/genmake2`.
So,
if you need to run :command:`genmake2` again,
make sure that you first do:

.. code-block:: bash

    $ module unload intel
    $ module unload intel/14.0/netcdf_hdf5

and then re-load the modules before running :command:`make`.
