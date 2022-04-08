Highlights Week 14

- SHREK / sPHENIX Production System / Design decisions / thoughts / plans
	- Discussions w/ Tadashi on the details of how PanDA utilizes common-workflow-language.  Some features (e.g. IntialWorkDir requirement) are difficult to support and will not be.  
	- So must rely on another path to support single document (per pass) job definition...  Job scripts can be created either before job submission or when the job lands on the worker node.  
	- Generating job scripts at point of submission is the prefered way... primarily b/c it defines the job against a fixed set of input codes and parser
	- Further discussions... he encouraged the use of github for archiving (already in plan) *and* for submission...  Which would imply that in order to submit a job, the inputs *must* orginate from a tagged github repo... no uncommitted codes...  
	- Additionally, all inputs must be cataloged and staged
	- (Submission rules can be overridden by a *test* option at submit time)
	- Finally, PanDA has a feature that cuts against documentation.  Specifically, on submission it automagically sends the contents of the current working directory to the worker node.  Would prefer to be specific about which directories / files / codes get transferred, so that this information gets encoded into the documentation.
	- CWL is still the prefferred language in which to express the full job definition / submission.  Idea is to run a CWL document that manages the staging, submission, documentation of the job.  
	- There are some awkward CWL behaviors, however.  These include that CWL runs in an empty environment by default, and runs in a separate directory from the submission point *by design*... (I don't see how to force it to run in the cwd...)
	- Strongly considering implementing shrek as a python command line application instead.
		- github api to interact with the repository
		- 