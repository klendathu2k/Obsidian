SHREK
- Achievment unlocked:  SHREK is now able to define workflows which execute under PanDA.  
	- Demonstrated using the [simple](https://panda-doma.cern.ch/tasks/?jeditaskid=65588|65587) workflow, with a "top" job feeding its output into a "bottom" job.  Works as expected.
	- More [complicated](https://panda-doma.cern.ch/tasks/?jeditaskid=65555|65557|1651600566|65556) example fails because the input datasets to the workflow do not exist.  Nevertheless, the "generation" parts of the example (which requires no output) run.  
- First attempt to run sPHENIX simulation workflow ran into snags... some additional understanding of the sPHENIX codes / outputs is required to define the workflow.
	1. Fun4All macros *mix* data analysis/simulation with file management
		- At the end of the processing, output files are staged to an output directory and entered into a DB
		- This breaks the PanDA workflow which expects to find the output files 
	    - Switching off the "production" option *also* switches off production of DST files required by the downstream codes...
	2. When I defined my first test definitions for the HF production, I was working under an assumption that each job would produce one output file that would then be fed into the next stage... 
		- looking further into the pass3* files, and looking into the "production" switch side effects... there are clearly other files being produced... so... 
		- I need to identify each of these files so they can be added to the output data set.
		- I need to make sure I understand PanDA's handling of these output files... b/c the input of the next job should take all of the outputs of the previous job... and not mix outputs from previous jobs...
		- This should require a round of testing...
	3. Given the above, there are a couple of ways to proceed to a full demonstration of sPHENIX workflow.
		- Identify (done) and hollow out (TBD) the macros which move the data.  Then implement the workflows in shrek/yaml files.
			- Still requires understanding of what files are produced
		- Add support for "optional" output files to shrek.  Then just map the existing sPHENIX workflow onto the shrek / yaml file definition.
			- Requires analysis of their condor submission scripts and understanding of how to map onto shrek / PanDA.
		- Not clear which of the two above options will be quickest... 


STAR 
Jinlong is having issues running pp 2015 embedding.  The simulation stage works.  (NOTE to self-- Resolution of the physics bug in that library should be checked b/c user reports memory option still required...)  But the embedding step is segmentation faulting...

This took some digging, but it appears that DBV timestamp used in the analysis chain is causing problems.

