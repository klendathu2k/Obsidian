Highlights Week 15

Small effort on STAR embedding bug.   The memory issue is still with us.  Can be worked around by increasing geant memory, but not clear that this is a good solution.   My recollection is that we have run into this in the past...  but not sure that that is relevant today.

SHREK

Settled on a preliminary design.  For each job in a workflow, users will implement a yaml file containing a complete definition of the job: input and output data sets, parameters to steer the code execution, macros and shell commands to execute them.  The workflow files to feed to the PanDA will either be 



-----------------------------------------------------------

(note to self... trying to recall.  Wasn't there a similar error back in the Prashanth era of the FMS?  Wasn't that a memory issue that he ran into during condor jobs that couldn't be reproduced interactively?  Why am I thinking about this now, after running tests which exclude the eta range of the FMS and still observing the issue?  Forget how this was resolved or worked around...)