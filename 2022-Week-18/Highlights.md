SHREK
- Achievment unlocked:  SHREK is now able to define workflows which execute under PanDA.  Demonstrated using the "simple" and "complicated" workflow examples provided in the PanDA docs.
- First attempt to run sPHENIX simulation workflow ran into snags... some additional understanding of the sPHENIX codes / outputs is required to define the workflow.
	1. Fun4All macros *mix* data production with file management
		- At the end of the processing, output files are staged to an output directory and entered into a DB
		- This breaks the PanDA workflow which expects to find the output files 
	    - Switching off the "production" option *also* switches off production of DST files required by the downstream codes...
	2. When I defined my first test definitions for the HF production, I was working under an assumption that each job would produce one output file that would then be fed into the next stage... 
		- looking further into the pass3* files, and looking into the "production" switch side effects... there are clearly other files being produced... so... 
		- I need to identify each of these files so they can be added to the output data set.
		- I need to make sure I understand PanDA's handling of these output files... b/c the input of the next job should take all of the outputs of the previous job... and not mix outputs from previous jobs...
		- 

- 
-   quick inspection of the Fun4All macros shows that they have a design issue... mixing-of-conerns.  
	- The Fun4All macros have code plugins which perform file management.
	- At the end of each job, files will be moved from the current directory to another location, and entered into a database
	- This breaks the PanDA workflow, b/c the files will be gone by the time the output dataset is formed
	- Switching off the "production" option in Fun4All has an additional side effect, that pileup and apparently ID truth (?) information will not be created.  These will 