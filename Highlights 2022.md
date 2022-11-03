geant4star timeline

10/2021
- Enabled geant.root persistency
- Mapping command line options to event generators (pythia6, 8)

12/2021
- Volume extensions --> map rather than using the TGeo extension mechanism (aiming for geant3 vmc and mixed engines)
- Found issue with geant3 SD implementation
	- [PR#34 @ VMC github](https://github.com/vmc-project/geant3/pull/34)
- Multiengine mode

01/2022
- Fix... track propagation cuts and options on all engines

02/2022
- Cleanup inconsistencies between geant4star development branch and main branch.

[geant4star status](https://drupal.star.bnl.gov/STAR/event/2022/02/09/SC-Management-Meeting/GEANT4-ROOT6-update) 02/09

[[geant4star status]] presented 03/15
[[geant4star status 04-20-2022]] presented 04/20/22
- The big PR #311

- [[2022-09-29]] Have split the code into preliminary chunk... working from there.

```
The geant4star application was developed in order to support the STAR forward physics program in runs 23+, enabling for the first time simulations based on the Geant 4 physics models. This is of particular utility in simulating the newly installed hadronic calorimeters in the forward direction.  
  
The goal is to integrate geant4star into the standard STAR code base, and work with  
stakeholders to perform initial physics evaluations.  
  
Milestones:  
- commit working source code for full codebase with geant4star added to git  
- provide a release in the EVAL area in afs  
- make pull request for the integration of geant4star on the main branch  
- responding to comments, break PR into smaller units  
- work with stakeholders to define QA metrics for the initial physics evaluations
```

With the completion of the STAR forward upgrade, the STAR experiment gains access to several observables at forward rapidity, such as jets, dijets, Drell-Yan dielectrons, and Lambda polarization.  These measurements are enabled by both the high precision tracking and calorimetry.  To fully maximize the physics impact of the forward hadronic calorimeter, an upgrade of STAR's simulation packages from GEANT3 to Geant4 is required.

Previously I have developed a Geant4 simulation within the STAR framework utilizing the virtual Monte Carlo simulation package.  The geant4star application demonstrated consistency with the MC event data model and compatability with the full STAR software stack.   Integration onto the main branch of the STAR software stack, and physics validation remained as open tasks.    

Before work began on these tasks, I decided to implement a new feature provided within the VMC framework: the ability to run *both* GEANT3 and Geant4 physics models in a single simulation run.  The advantage of this approach is that the midrapidity physics simulation can remain (essentially) unchanged compared with prior phsyics analyses, while the forward physics program can leverage the improved hadronic physics simulation afforted by Geant4.  Further, it enables direct comparison between G3 and G4 physics observables at midrapidity, which will help in tuning the G4 physics lists in the future.

In implementing this feature, I had to overcome three issues.  First, the representation of AgML extended geometry information used in truth tagging had to be reshaped due to the use (abuse) of the TGeoExtension mechanism by the GEANT3 VMC developers.  Second, track propagation cuts and physics options had to be implemented consistently for both the G3 and G4 physics engines.  Importantly, default values had to be made consistent with those utilized in *starsim*.  And third, a design issue with the GEANT3 VMC application was identified and fixed.  A contribution back to the VMC project was made:
[1] https://github.com/vmc-project/geant3/pull/34

Milestones:  
- commit working source code for full codebase with geant4star added to git  
- make pull request for the integration of geant4star on the main branch  
- responding to comments, break PR into smaller units  
	- Codes were assembled on a (rather large) integration branch for review.   Reviewers recommended breaking into smaller pull requests.  First such PR is focused on infrastructure (loading geant, vmc libraries) and should be reshaped to utilize a recent change in the infrastructure to support changes to the environment through spack.  
	- Final integration onto the main branch will likely require migration of the STAR software stack to ROOT 6.  Or alternatively, supporting geant4star with a seperate build of the software stack.
- provide a release in the EVAL area in afs  
- work with stakeholders to define QA metrics for the initial physics evaluations
	- This was performed using the code in the initial pull request.  Some discussion with stakeholders about physics evaluations began.  But due to the physics run, workforce was not available.  


Moving forward, we still need to integrate with the full STAR software stack and perform a physics evaluation.  Integration will lower the threshold for stakeholders to perform such studies.  And integration will required migration to ROOT 6.

StEvent Maintence

- Took over responsability for STAR EDM 03/2022
- Forward Upgrades data structures
	- Reviewed StEvent proposals... found issue with adding GenFit dependency
	- 

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

```
**Description/Milestones**: The sPHENIX computing model requires a production system which can handle the envisioned complicated workflow, involving multiple passes of track finding, fitting and distortion corrections in parallel with calorimetry reconstruction. To this end the collaboration has selected PanDA as its workflow management system and Rucio as its data mangement system.  
  
The production system will be responsible for submitting reconstruction jobs to PanDA as the data becomes available, documenting the datasets produced and the codes which have been run and under what conditions, and ensuring that data samples can be reproduced at future dates.  
  
1. Demonstrate sPHENIX workflows running on PanDA  
2. Develop a package which can document the reconstruction jobs which are run  
3. Verify that data processing runs at scale  
4. Work towards supporting the ongoing mock data challenge(s) with a prototype production system  
5. Work with stakeholders to refine the system with an eye towards supporting experimental operations from day one
```

SHREK, the sPHENIX Handy Remote Execution Koordinator (working title), is being developed to manage the data productions of the sPHENIX experiment.  It consists of several components.  (1) A job description language, (2) a job submission script, and (3) a monitoring and dispatch service.  These components are used as a frontend to the PanDA workflow management system.

The job description language is implemented in YAML, allowing users to specify in a single text filethe input and output datasets to a job, the location of required job artefacts (eg macros), and the job script (bash) which will execute on the remote service.  The job description language allows all parameters for the job to be defined in a single file (this includes both user's parameters, as well as any PanDA options which need to be specified.)   The job submission script parses one or more job description files, creates the common workflow language document that PanDA uses to steer the workflow, and assembles the job artefacts within a job submission directory.  Optionally the submission directory can be archived on github for documentation purposes.  Finally, a monitoring and dispatch service (aka "donkey") has been implemented, which can poll a file managment resource (eg rucio) and launch user-specified actions (eg sumit a job to PanDA) when datasets matching certain criteria become available.

Milestones
- Demonstrate sPHENIX workflows running on PanDA  
- Verify that data processing runs at scale  
	- The complete heavy-flavor charm simulation, including pileup simulation and event reconstruction, has been implemented.
	- I have shown that the code runs at scale, executing over the full time 
- Develop a package which can document the reconstruction jobs which are run  
- 
- Work towards supporting the ongoing mock data challenge(s) with a prototype production system  
- Work with stakeholders to refine the system with an eye towards supporting experimental operations from day one
