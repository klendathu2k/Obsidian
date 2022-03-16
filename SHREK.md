# The sPHENIX Handy Remote Execution Koordinator

![SHREK](https://lh4.googleusercontent.com/G5w4P1uwUYpU-ObA8T3fDdm27jEm66IxTQ-sHTB8_LGZQbZpQK4xGBMeMpDTHxCBIPt9_vnBkuWdjTYcaTGBhjLEMC4giqNX_YLv9d5RR6G4mJgOiw9O9e1q4l-GcA1dZMVp1Nl-) 


[sPHENIX Distributed Computing Meeting Document](https://docs.google.com/document/d/1L8DAzhCwpVoRM_WptpZFKqJev4-odk4xDl5rDK6JMYs/view)

## Design Goals
- Reproducibility
- Support documentation generation
- Provide *single source description* of the job workflow
	- Unlikely to be able to provide a single source description b/c there will be multiple input files (steering macro, CWL for PanDA, CWL for steering file staging, etc...)
	- So the requirement needs to shift to *tagging* of the jobs
	- But see [[#^517f5f]]... files can be created at run time


## Design Narrative
The prodution system should be designed to support the needs of a nuclear physics experiment, enabling documentation of  job workflows and reproducible results.  The production system must interact with job scheduling software [PanDA](https://panda-wms.readthedocs.io/en/latest/) and file management [Rucio](http://rucio.cern.ch/documentation/), as well as local file catalog.

## PanDA notes

- [Setting up PanDA](https://docs.google.com/document/d/1L8DAzhCwpVoRM_WptpZFKqJev4-odk4xDl5rDK6JMYs/edit#bookmark=id.z1x615fzlkkw)
- [Running simple jobs](https://panda-wms.readthedocs.io/en/latest/client/prun.html)
	- Use the instructions for DOMA users
	- Allows one to execute simple linear workflows (anything that can be executed as a batch script)
	- Command line options to flag input and output data sets /
	- Should use the --noBuild option
- [Running Workflows](https://panda-wms.readthedocs.io/en/latest/client/pchain.html)
	- Uses pchain command /  Common workflow language [[#^b9e7f8]] to specify jobs.
	- When running *prun* directly, the local computer is submitting the jobs to PanDA.  
	- When running pchain... *I think* that prun is executing on a remote server, under the control of a CWL implementation / runner.  

[[PanDA Links]]

## Rucio Notes

## Common Workflow Language
The [Common Workflow Language](https://www.commonwl.org/) is a json and YAML based language which can be used to specify multiple, dependent jobs in a workflow that correspond to a directed acyclic graph, with each individual compute task represented by a node in the graph. ^b9e7f8

### Useful features
[Create files at runtime](https://www.commonwl.org/user_guide/14-runtime/index.html) ^517f5f


## sPHENIX Production Chain Notes
![[Pasted image 20220314120142.png]]

Fun4All is a software package whose operation is *steered* by ROOT macros.  Unlike the STAR software, which makes heavy use of a single ROOT macro (the Big "Friendly" Chain) to drive reconstruction jobs, F4A implements custom production macros when any global configuration changes.  (eg different tracking module, different clustering algorithms, etc...).  Note that my understanding / knowlege of this can / should evolve.

But... bottom line is that the *macro itself* becomes part of the job documentation, rather than a long list of chain options.

So... rather than maintaining a single steering macro which accepts an easily documented list of chain options, sPHENIX has chosen to implement production specific steering macros.

### Production Tagging Convention
Each data production campaign should be uniquely identifiable through a single tag.  That tag should serve as a searchable index, allowing the user to recover all production artifacts, as well as to reproduce the data sample from the documented inputs.  Thus, the tag should minimally contain the following:

- Tag should contain the software library / build reference e.g. mdcX.Y
- Tag should note whether it is a simulation job, reconstruction job, ... (embedding?)
- Tag ought to be lightweight and infomative

- Each data production campaign should be uniquely identified...
	- The tag should have a unique identifier, which encodes the year of the production
	- A unique string to distinguish multiple productions per year
	- A job identifier to specify what type of job is being carried out
	- A build / release identifier to specify the 
	
- sP *YY* *ab* - *type* - *build*
	- sP for sPHENIX
	- YY two digit year
	- ab alphanumeric two digit *unique* job identifier
		- Ordering is as follows: 
		- abcdefghijklmnopqrstuvwxyz1234567890
			- aa ... zz a1 ... z0
		- capital letters are reserved for testing purposes, and have inverted order
			- ZZ ... AA .. Z1 .. Z0  and should not be searchable
	- type of job (S simu, R reco, E embed, T test, C calibration set...)
		- type may be accumulated, so SR is a simulation job with reconstruction, SRT test simulation with reconstruction, RC is reconstructed 
	
	Example tag:
	
	sP22aa-SRM-mdc2.4 -- sPHENIX simulation "aa" is the first of the year, uses mdc2.4 library.
	
	Would correspond to job submission files...
	
	- Workflows will use the full tag
		sP22aa-SRM-mdc2.4.cwl -- CWL PanDA input
		sP22aa-SRM-mdc2.4.yml -- corresponding yaml file
	
	- Payload files should *all* utilize the short tag in their name
		sP22aa_Fun4All_pass1.C 
		sP22aa_Fun4All_pass2.C
		...
		sP22aa_Fun4All_passN.C
		
	- Job directories shold use the full tag
		- Should have a layout directory along the lines of
		
		sP22aa-SRM-mdc2.4/input   -- contains filelists for input
		sP22aa-SRM-mdc2.4/output -- output manifest
		sP22aa-SRM-mdc2.4/log       -- log file manifest
		sP22aa-SRM-mdc2.4/job       -- job specification and submission directory
		sP22aa-SRM-mdc2.4/dev      -- (optional) job *development* directory		
		sP22aa-SRM-mdc2.4/README.md -- long description of the production
		
	- The job directories would most naturally be folded into a github repository
	- IF the tag is complete enough, could automate creation of a job template.

- Use of the YAML file to define tags / directories / etc... 


## Documentation Web Page

Consider the use of [github pages](https://docs.github.com/en/pages) to host documentation.  Would basically be looking for a tabular form which would look like


| TAG [README] | directory | notes |
| ---- | --------- | ----------------------------------------------------------|
| sP22aa | sP22aa-SRM-mdc2.4/ | pythia8 200 GeV pp simulation for MDC          |
| sP22ab | sP22ab-SRM-mdc2.4/ | pythia8 200 GeV pp simulation for MDC w/ pileup|
| ...... | .......... | ...... |
| sp22iz| sp22iz-R-auau22.1 | Run 22 AuAu reconstruction set |

github pages has a 1GB limit... so this has to be pretty lightweight.   So the directory structure that gets pushed to github should only contain mainifest files...



	
## New strategy... copy back direct / copy in direct
- Avoids using PanDA's output / input strategy and just copy the files in direct from the filesystem... *this* **is** ***NAUGHTY***... use rsync, limit the number of jobs, and pray that it does not break things.
- Will want to control the jobs via environment variables... [CWL environment](https://www.commonwl.org/user_guide/12-env/index.html)  ... so that to modify the job only need to change the YAML file.
- Will use a shell script for each pass
- Now I need to know whether pass2 depends on pass1 or not... (try to answer myself before spamming Chris... need to familiarize with the codes, and this is a starting point, ... but don't waste too much time this afternoon...
	- Takes a list of background files... not yet sure where that is defined...
	- OMFG they use a perl script.  
		- Background list is a set of files pulled in from a file catalog query...
	- So.... pchain will need to stage background files...  And I think it will be a workflow that looks more like the following...

	![[Pasted image 20220316140833.png|400]]
	
	- The CWL file should specify two jobs which are independent of each other... pass1 and pass2.fetch, followed by the pass2.merge operation.
	- Having trouble handling non-string inputs....
		- May need to use a javascript expression in the workflow ...
		- ... may need to install Node.js ...
		- For now... just cast these to strings... they are destined for environment variables anyhow
		- Actually... integer types are handled differently than strings... $(inputs.stringy) versus inputs.integery
		
		

	
## Test simple chain / PanDA
[simple task chain](https://panda-wms.readthedocs.io/en/latest/client/pchain.html#simple-task-chain)

...

pchain --cwl simple.cwl --yaml dummy.yaml --outDS user.jwebb2.`uuidgen` --vo wlcg --prodSourceLabel test --workingGroup sphenix

... 

Creates a chain of jobs via PanDA.  Directory structure will be formed based on the outDS arguement.

[user.jwebb2.584aef2c-a9b3-4e10-8aea-690c5ed3fd17_000_top](https://panda-doma.cern.ch/task/10836/)

	pchain --cwl simple.cwl --yaml dummy.yaml --outDS sP22ZZ-T-none --vo wlcg --prodSourceLabel test --workingGroup sphenix

ERROR : outDS must be 'user.jwebb2.<user-controlled string...>'
	
So... need to use something like
	
	pchain --cwl simple.cwl --yaml dummy.yaml --outDS user.jwebb2.sP22ZZ-T-none --vo wlcg --prodSourceLabel test --workingGroup sphenix

	Executing with --check option dumps a json stream that specifies the output directory structure.
	
	The output directory structure reflects the division of jobs specified in the workflow.
	
	May be useful to capture this ... wrap pchain with a python script that will first run with --check option, capture the json output, and then run the actual submission.
	
	
	https://panda-doma.cern.ch/tasks/?jeditaskid=10839&status=broken&status=broken
	
	"failed to get files for user.jwebb2.sP22ZZ-T-none_000_top_seed.txt/"
	
	Looks like the bottom job cannot find the top job's output?  Test by trying to return the top output.
	
	Taking an abnormal amount of time in the "running" state, but otherwise the "hello world" is not failing.
	
	Try removing any inter-job data dependency
	
	... not seeing the test job in the monitor?
	
	
	
	
	
	






## Weeks 10 - 11 
-   Next step: focus on pp production with full downstream simu/reco workflow, and data flow (getting files back)
	-   address how to add Rucio registration? Jobs write directly to shared file space. So PanDA knows instance locations as well as LFNs. PanDA does the necessary registration.
-  Target for next meeting in 2 weeks   
	-   be ready to switch simu production to PanDA. Would be simpler than what Chris is currently doing.

Goal for this work period is to demonstrate *pchain* based simulation production using the 2-pass pp200 GeV simulation for the current MDC.  Chris has handed me the workflow, ... covering two passes.  An initial simulation, producing N hits files.  And a follow on pass2 pileup simulation, producing N hits files w/ pileup.
- Question: how is the pileup simulated?  
	- --> pass 1 file plus pre-generated background files
	

	
	