ROOT6 / Geant4star Integration

- Able to build the STAR software stack against root 6.16.00 using the new STAR environment with spack module support provided by Dmitri / Jerome... PR by Daniel.
	- Required modification of the star v0.23 environment, with explicit specification of the root 6.16.00 version
	- Removed StiCA and TPPCAtracker components b/c I did not want to spend time figuring out which version of VC needed to be loaded
* Small set of unit tests setup
	* Required fix to geometry interfaceReworked the macros which instantiate the STAR geometry to workaround a limitation in ROOT6 which prevented the geometry files from being loaded
		- [PR 422](https://github.com/star-bnl/star-sw/pull/422) 
- Verified that the *starsim* application runs (it is standalone FORtran code so no suprise there)
- Run a simulation (geant3 / starsim) through the big full chain
	- Identified / resolved an issue in the BFC.C macro which prevented runtime initialization of the big full chain
		- [PR 423](https://github.com/star-bnl/star-sw/pull/423)
- 	-