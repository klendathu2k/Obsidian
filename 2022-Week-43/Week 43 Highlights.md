ROOT6 / Geant4star Integration

- Able to build the STAR software stack against root 6.16.00 using the new STAR environment with spack module support provided by Dmitri / Jerome... PR by Daniel.
	- Required modification of the star v0.23 environment, with explicit specification of the root 6.16.00 version
	- Removed StiCA and TPPCAtracker components b/c I did not want to spend time figuring out which version of VC needed to be loaded
* Verified that the *starsim* application runs (it is standalone FORtran code so no suprise there)
* Small set of unit tests setup
	* Running simple macros, loading shared libraries, etc...
	* Loading AgML geometry... required fix to interface macros 
		- [PR 422](https://github.com/star-bnl/star-sw/pull/422) 
- Run a simulation (geant3 / starsim) through the big full chain
	- Identified / resolved an issue in the BFC.C macro which prevented runtime initialization of the big full chain
		- [PR 423](https://github.com/star-bnl/star-sw/pull/423)
	- First attempt running an example macro 