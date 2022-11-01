ROOT6 / Geant4star Integration

- Able to build the STAR software stack against root 6.16.00 using the new STAR environment with spack module support provided by Dmitri / Jerome... PR by Daniel.
	- Required modification of the star v0.23 environment, with explicit specification of the root 6.16.00 version
	- Removed StiCA and TPPCAtracker components b/c I did not want to spend time figuring out which version of VC needed to be loaded
- [PR 4]