geant4star timeline

[[geant4star status]] presented 03/15
[[geant4star status 04-20-2022]] presented 04/20/22
- The big PR #311


StEvent Maintence

- Took over responsability for STAR EDM 03/2022

SHREK timeline
- 03/21 Week -- Clarified w/ Tadashi the usage of CWL in PanDA is limited.  
	- i.e. cannot generate files, have to have the full workflow packaged and ready on the submission node.
- 03/28 Week -- Prototyped yaml job definition
	- [[sPhenix Handy Remote Execution Coordinator 1]]
		- Hrmmm.... was still considering a pure CWL solution at this point?
		- Began developing a tagging convention (putting the cart before the donkey here...)
- [[Highlights Week 14]]
	- Converging on YAML file description of the jobs...
	- [[SHREK Preliminary Design]]
	- Heavily influenced on STAR [SUMS](https://www.osti.gov/servlets/purl/1479267) XML description of jobs
	- Additional wrinkle that SHREK should manage multiple interdependent jobs (i.e. a workflow) rather than a straight lineral chain of jobs handled by SUMS.
	- 


