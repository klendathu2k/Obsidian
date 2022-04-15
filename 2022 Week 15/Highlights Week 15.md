Highlights Week 15

Small effort on STAR embedding bug.   The memory issue is still with us.  Can be worked around by increasing geant memory, but not clear that this is a good solution.   My recollection is that we have run into this in the past...  but not sure that that is relevant today.

## SHREK

### Settled on a preliminary design.  

For each job in a workflow, users will implement a yaml file containing a complete definition of the job: input and output data sets, parameters to steer the code execution, macros and shell commands to execute them.  User job execution scripts will be dynamically created during job submission, and uploaded to the remote resource.

Layout of the input files and supporting codes will be up to the user (in the production context, there will be a convention for how the directory structure maps onto the workflow.)

The workflow *can*  be created dynamically as well from the yaml inputs.  Should be simply a matter of building the graph of nodes=jobs edges=(output-->input).  But some words of wisdom from Star Trek VI... just because we can do a thing, it does not necessarily follow that we must do that thing.  So first I should setup workflow templates.  Inputs, outputs, job scripts are the template parameters, filled in by shrek.

### Input file schema

Established a schema for the job defintion files:
https://github.com/klendathu2k/shrek/tree/schema/schema

Implemented tests which validate the schema.



-----------------------------------------------------------

(note to self... trying to recall.  Wasn't there a similar error back in the Prashanth era of the FMS?  Wasn't that a memory issue that he ran into during condor jobs that couldn't be reproduced interactively?  Why am I thinking about this now, after running tests which exclude the eta range of the FMS and still observing the issue?  Forget how this was resolved or worked around...)