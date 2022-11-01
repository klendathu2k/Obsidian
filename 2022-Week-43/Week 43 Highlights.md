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
	- First attempt running [example macro](https://github.com/star-bnl/star-sw/blob/main/StRoot/StarGenerator/macros/starsim.kinematics.C)
		- Fails...
	- *Significantly* reworked the macro until it ran... 
	- Analyzed why...

We will have a significant issue with running many STAR macros unmodified.  Most specifically in our simulation and embedding macros.  We follow a typical idiom...

```
*bfcRunner.C*
0001 | StChain* chain1=0;
0002 | StChain* chain2=0;
0003 | // ...
0004 | macro bfcRunner() {
0005 | 
0006 |   gROOT->LoadMacro("bfc.C")
0007 |   bfc(-1,"<list of chain options>");
0008 |   chain1 = chain;
0009 |   bfc(-1,"<another list of chain options");
0010 |   chain2 = chain;
0011 |   // ...
0012 |   StAnalysisMaker* mk = chain->GetMaker("analysis");
0013 |   mk->setSomething("blah",1);
0014 |   // ...
0015 | 
0016 | }
```

The `bfc.C` macro mixes several concerns: (1) loading shared libraries, (2) and the ROOT dictionaries, (3) creating the hierarchy of makers (aka the analysis chain).  

ROOT5 (CINT interpreter) and ROOT6 (cling compiler / interpreter) behave very differently when processing macros.  ROOT5 interprets the macro line-by-line.  So on line 0007, the bfc macros loads in all of the shared libraries specified by the chain options *and* the corresponding root dictionaries.  This makes available to the interpreter the symbols needed to access the analysis maker and other user codes within the macro and perform run time configuration.  

Essentially the bfc.C macro *loads shared libraries and root dictionaries at run time.*

ROOT6 is *compiles the full macro*.  But he shared libraries / dictionaries are loaded at run time.  Even if we include the header files (to create the interface to the user codes)... ROOT6 will still not be able to compile / link the macro because the shared library containing the StAnalysisMaker has not been loaded.   Our standard macros cannot be run without heavy modification, because the `bfc` calls have to be resolved before 