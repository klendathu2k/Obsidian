 ### sPHENIX Production System
 
 ![SHREK](https://lh4.googleusercontent.com/G5w4P1uwUYpU-ObA8T3fDdm27jEm66IxTQ-sHTB8_LGZQbZpQK4xGBMeMpDTHxCBIPt9_vnBkuWdjTYcaTGBhjLEMC4giqNX_YLv9d5RR6G4mJgOiw9O9e1q4l-GcA1dZMVp1Nl-) 
 
 ---

### Design Goals
- Reproducibility
- Documentation / Bookkeeping

--> Provide *single source description* of the job workflow
	 
---

Tagging convention
- Associate all production inputs and outputs with a concise label
![[Pasted image 20220323125215.png]]

---

CWL --> [Common Workflow Language](https://www.commonwl.org/)

- Build complex parallel workflows from simple command line tools... 
- Use with PanDA may come with limitations...

---

### Try to come up with a good name...
Coordinate the Remote Execution of sPHENIX Data Productions...

---

sPHENIX Handy Remote Execution Koordinator (*working title*)
![[Pasted image 20220323093933.png|400]]



---


---

Important to note:
- CWL is used by *panda* to run *prun tasks* on the remote PanDA server

- all production codes must be wrapped by a script which 
	- sets up the environment
	- manages job parameters (such as run number, sequence/RNG number, etc...), some of which are generated per job by PanDA

---

### First attempt: MDC Pythia HF Workflow

- pass1 - generate HF pythia events
- pass2 - merge pythia events with pre-generated 

![[Pasted image 20220316140833.png|400]]

---

> run_hfprod.sh *build* *nevents* *type* *job name* *output directory* *run number* *sequence number*

Inside of run_hfprod.sh stdout is redirected to /sphenix/user/sphnxpro/out.txt

---

`prun --exec "run_hfprod.sh mdc2.7 1 Charm TestSimulation ./ 1234567890 %RNDM:00001" --outDS user.jwebb2.`uuidgen` --noBuild --vo wlcg --site BNL_OSG_SPHENIX --prodSourceLabel test --workingGroup ${PANDA_AUTH_VO} --maxAttempt 1 --followLinks --cpuTimePerEvent=1200 --maxWalltime 24 --memory 2048`

[Task 11014](https://panda-doma.cern.ch/task/11014/)

---

> $ tail -n 28 /sphenix/user/sphnxpro/out.txt | grep *.root
>  .rootrc
> G4Test_Charm-1234567890-00002.root

---

## Current status

1. pass1 runs and can be scaled to more nevents and jobs
2. root files *can* be copied back to /sphenix/users/sphnxpro directly...
	-	would prefer to stage back via rucio ...
3. next step is to get pass2 up and running




