Running MITgcm on multiple processors
=====================================

The main source of information is the model's manual compilation section: http://mitgcm.org/public/r2_manual/latest/online_documents/node94.html .
You can get the code from MITgcm.org via CVS. 

Compile the code:

As described on the documentation, MITgcm uses the "make" program to compile the code. MITgcm provides a script genmake2 that creates a makefile used by make. This file allows the model to pre-process source files, specify the compiler and figure out dependencies.
Afterwards, you need to build the dependencies and compile the code. 

Again, there is a detailed explanation of how to build the code in the documentation above.

Specific hints and instructions for mpi runs
--------------------------------------------
The two machines where we have run MITgcm in multiple processors are Westgrid's Bugaboo and Salish. The optfiles for each machine are under the optfiles repo. They have been adapted from other example optfiles on the MITgcm website.

Tips and hints for Westgrid's Bugaboo

 * optfile: bugaboo_mpi.opt.


Tips and hints for Salish

 * optfile: salish_mpi.opt
 * To avoid broken pipe errors, execute mitgcmuv on the background (use & at the end of the mpi run command) and exit the session. If you want to monitor the process, start a new session.
 
 




