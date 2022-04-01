 ### sPHENIX Production System
 
 ![SHREK](https://lh4.googleusercontent.com/G5w4P1uwUYpU-ObA8T3fDdm27jEm66IxTQ-sHTB8_LGZQbZpQK4xGBMeMpDTHxCBIPt9_vnBkuWdjTYcaTGBhjLEMC4giqNX_YLv9d5RR6G4mJgOiw9O9e1q4l-GcA1dZMVp1Nl-) 
 
 ---

### Design Goals
- Reproducibility
- Documentation / Bookkeeping

--> Provide *single source description* of the job workflow
	 
---

Tagging convention
- Associate all production inputs and outputs with a unique, concise label
![[Pasted image 20220323125215.png]]
- Suitable for archiving on (e.g.) github

---

### First attempt: MDC Pythia HF Workflow

- pass1 - generate HF pythia events
- pass2 - merge pythia events with pre-generated 

![[Pasted image 20220316140833.png|400]]

... reconstruction passes to be implemented next

---

`prun --exec "run_hfprod.sh mdc2.7 1 Charm TestSimulation ./ 1234567890 %RNDM:00001" --outDS user.jwebb2.`uuidgen` --noBuild --vo wlcg --site BNL_OSG_SPHENIX --prodSourceLabel test --workingGroup ${PANDA_AUTH_VO} --maxAttempt 1 --followLinks --cpuTimePerEvent=1200 --maxWalltime 24 --memory 2048`

[Task 11014](https://panda-doma.cern.ch/task/11014/)

---

> $ tail -n 28 /sphenix/user/sphnxpro/out.txt | grep *.root
>  .rootrc
> G4Test_Charm-1234567890-00002.root

---

```
pchain -cwl shrek/shrek.cwl -yaml sP22aa-mdc2.7/job/hfprod-pass1.yaml \
       --outDS user.jwebb2.sP22aa-mdc2.7 \
	   ...
```

---

sPHENIX Handy Remote Execution Koordinator (*working title*)
![[Pasted image 20220323093933.png|400]]


### Current status

1. pass1 runs and can be scaled to more nevents and jobs
2. root files *can* be copied back to /sphenix/users/sphnxpro directly...
	-	would prefer to stage back via rucio ...
3. next step is to get pass2 up and running




