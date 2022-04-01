 ### Towards a Production System for sPHENIX
 
 ![SHREK|900](https://lh4.googleusercontent.com/G5w4P1uwUYpU-ObA8T3fDdm27jEm66IxTQ-sHTB8_LGZQbZpQK4xGBMeMpDTHxCBIPt9_vnBkuWdjTYcaTGBhjLEMC4giqNX_YLv9d5RR6G4mJgOiw9O9e1q4l-GcA1dZMVp1Nl-) 
 
 ---

### Design Goals
- Reproducibility
- Documentation / Bookkeeping

--> Provide *single source description* of the job workflow
	 
---

### First attempt: MDC Pythia HF Workflow

- pass1 - generate HF pythia events
- pass2 - merge pythia events with pre-generated 

![[Pasted image 20220316140833.png|400]]

... reconstruction passes to be implemented next

---

[Task 11014](https://panda-doma.cern.ch/task/11014/)

```
prun --exec "run_hfprod.sh mdc2.7 1 Charm TestSimulation ./ 
             1234567890 %RNDM:00001" 
	 --outDS user.jwebb2.`uuidgen` --noBuild --vo wlcg 
	 --site BNL_OSG_SPHENIX --prodSourceLabel test 
	 --workingGroup ${PANDA_AUTH_VO} --maxAttempt 1 
	 --followLinks --cpuTimePerEvent=1200 --maxWalltime 24 
	 --memory 2048
```


---

```
$ tail -n 28 /sphenix/user/sphnxpro/out.txt | grep *.root
 .rootrc
G4Test_Charm-1234567890-00002.root
```

---

 ![SHREK](https://lh4.googleusercontent.com/G5w4P1uwUYpU-ObA8T3fDdm27jEm66IxTQ-sHTB8_LGZQbZpQK4xGBMeMpDTHxCBIPt9_vnBkuWdjTYcaTGBhjLEMC4giqNX_YLv9d5RR6G4mJgOiw9O9e1q4l-GcA1dZMVp1Nl-) 

---

![[Pasted image 20220401095632.png|400]]

```
pchain -cwl shrek/shrek.cwl -yaml sP22aa-mdc2.7/job/hfprod-pass1.yaml \
       --outDS user.jwebb2.sP22aa-mdc2.7 \
	   ...
```


---

- Generic CWL "working" standalone under cwl-runner (no pchain submission)
- Testing submission to PanDA today... 
	- suspecting undocumented limitations running CWL on PanDA server...

---

sPHENIX Handy Remote Execution Koordinator 
![[Pasted image 20220323093933.png|400]]

---

### Current status

1. pass1 runs with direct submission with prun
	- root files *can* be copied back to /sphenix/users/sphnxpro directly...
	- would prefer to stage back via rucio ...
2. no show stoppers for pass2...
3. working to generalize so that the job description is expressed as a single yaml file input to pchain... (more discussion on Wednesday)

---

Tagging convention
- Associate all production inputs and outputs with a unique, concise label
![[Pasted image 20220323125215.png]]
- Suitable for archiving on (e.g.) github

---

