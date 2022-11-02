geant4star timeline

10/2021
- Enabled geant.root persistency
- Mapping command line options to event generators (pythia6, 8)

12/2021
- Volume exten

[[geant4star status]] presented 03/15
[[geant4star status 04-20-2022]] presented 04/20/22
- The big PR #311

- [[2022-09-29]] Have split the code into preliminary chunk... working from there.


StEvent Maintence

- Took over responsability for STAR EDM 03/2022

SHREK timeline
- 03/21 Week -- Clarified w/ Tadashi the usage of CWL in PanDA is limited.  
	- i.e. cannot generate files, have to have the full workflow packaged and ready on the submission node.
- 03/28 Week -- Prototyped yaml job definition
	- [[sPhenix Handy Remote Execution Coordinator 1]]
		- Hrmmm.... was still considering a pure CWL solution at this point?
		- Began developing a tagging convention (putting the cart before the donkey here...)
- [[Highlights Week 14]] 4/4
	- Converging on YAML file description of the jobs...
	- [[SHREK Preliminary Design]]
	- Heavily influenced on STAR [SUMS](https://www.osti.gov/servlets/purl/1479267) XML description of jobs
	- Additional wrinkle that SHREK should manage multiple interdependent jobs (i.e. a workflow) rather than a straight lineral chain of jobs handled by SUMS.
* [[Highlights Week 15]] 4/11
	* Preliminary design choice... each job in a workflow specified by a YAML document.
	* Build the CWL for pchain input by analyzing the YAML files to establish the graph with outputs --> inputs
	* Established the schema for the yaml files...
		* Think this still had some development work
* [[Highlights Week 16]]
	* ~90% towards a working example chain
- [[SHREK Status 04-27-2022]]
	- Job definition layer on top of PanDA / Rucio
- [[Highlights Week 18]]
	- First workflows executing on PanDA (simple examples)
-  [[Highlights Week 19]]
	- HF Workflow implementation work begins
	- Many scrapes and scars wrestling with the PanDA...
- [[Highlights Week 20]]
	- Ran into mistake in PanDA pchain documentation.
![[Pasted image 20220517131111.png]]
- Week 21... the PanDA has issues (and no unit tests?)
- Week 22... shortened week (memorial day weekend)... still have PanDA side issues
- Week 23... still stalled on the PanDA side
- Week 24 ... push job artefacts to github repository.
	- Should note that this is not entirely

... Lost it for a bit ...

- [[Highlights Week 30]] Week 30 (07/25)
	- SHREK implemeted resuable secondary stream
	- Begin scaling tests... (long saga...)
	- First attempts playing with rucio
		- Intermediate products are persistent...
-  Week 31  (08/01)
	- Wall clock issue identified
	- Discussion w/ Chris on distortion corrections...
	- 10% of each run to be processed for calibration purposes before full reconstruction gets launched... Exact layout TBD
- Week 32 (08/08)
	- Updated to more recent sPHENIX workflows
- Week 33 (08/15)
	- Debugging some filename issues w/r to the new workflows
- [[2022-08-22]] Week 34
	- More PanDA instability... scaling tests ... running into wall
- Week 35 (08/29)
	- Mapped command line arguements to shrek variables (both in the executive scripting and dataset definitions)
- Week 37... donkey implementation [[2022-09-12]]
- Week 38 (09/19)...
	- Beginning to think constant reauth to both PanDA DOMA and github is a pain in the butt.  Beginning to rethink doc / persistency
- Week 39
	- Walltime limit includes a x2 safety margin... remember, this is a user-centric rather than a production-centric system.  User will quote time *a* job takes to complete... and PanDA assumes that to be the mean time.  Wants all jobs to complete... x2 safety.  (Jeesh).
	- 
- Week 40 
	- Scaling up to arbitrary size should work from this point forward.
	- PanDA is on the fritz again...
	- Shifting back to STAR