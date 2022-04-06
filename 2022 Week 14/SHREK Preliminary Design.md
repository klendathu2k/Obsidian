SHREK Preliminary Design

---

Design Goals
---

-  Reproducibility
- Support documentation generation
- Provide *single source description* of the job workflow

---

Single Source 
---
- Goal is to *minimize* PBCK errors.
- Minimize number of files the production manager needs to touch to deine and run the job.   
- One definition file per pass...

PBCK = Problems Between Chair and Keyboard

---

![SHREK](https://lh4.googleusercontent.com/G5w4P1uwUYpU-ObA8T3fDdm27jEm66IxTQ-sHTB8_LGZQbZpQK4xGBMeMpDTHxCBIPt9_vnBkuWdjTYcaTGBhjLEMC4giqNX_YLv9d5RR6G4mJgOiw9O9e1q4l-GcA1dZMVp1Nl-) 

---

![[Pasted image 20220406105236.png|400]]

---

![[Pasted image 20220406105537.png|600]]

---

SHREK will provide user- and system-generated environment variables needed to map the user workflow onto the PanDA submission

---

```
$ cat run_hfcharm_pass1.yaml

# Specifies a unique name for the job                                  
jobname: g4charm_pass1      

# Input data sets
input_ds: null

# Extra panda flags (such as number of jobs to run)              
extra_panda_args: --nJobs 5                        

# sPHENIX software build level 
build: mdc2.7                                                           

# Job parameters
nevents: 100    # to generate                                            type: Charm     # type of job     
outfile: TestSubmission   
outdir: /sphenix/user/sphnxpro/shrek/pass1/out  
logdir: /sphenix/user/sphnxpro/shrek/pass1/log  
jobdir: /sphenix/u/jwebb2/work/2022/SHREK/MDC2 

runnumber: 1234567890 

# Commands to stage files required to run the code (semi-naughty)
stagecmd: |-                                                          
  ln -s /sphenix/u/jwebb2/work/2022/SHREK/MDC2/submit/HF_pp200_signal/pass1/rundir/* .                                                   
                                        
# Command block                                                        
commands: |-            
  
   export infiles=$1
   run_hfprod_pass1.sh $SHREK_build \
                       $SHREK_nevents \
                       $SHREK_type \
                       $SHREK_outfile \
                       $SHREK_outdir \
                       $SHREK_runnumber \
                       $SHREK_jobindex
  
# Copy back block (for naughty copies...)
copyback: |-           

  export manifest = ${SHREK_jobname|-${SHREK_tag}-${SHREK_runnumber}-${SHREK_jobindex}.manifest

  echo "JOB ${SHREK_jobindex} of ${SHREK_nJobs}">>${manifest}

  ls *.root >> ${manifest}
  cp ${manifest} ${SHREK_outdir}

```

---

![[Pasted image 20220406113612.png|500]]

SHREK maps the user- and system-defined parameters onto environment variables with which users can steer their code


---

![[Pasted image 20220406113612.png|500]]

SHREK does not play well with PanDA...
```
pchain --cwl shrek.cwl --yaml passN.yaml
```
... does not work b/c SHREK uses CWL features that PanDA cannot support...


---

![[Pasted image 20220406113612.png|500]]

SHREK will eventually get along with anyone...
```
prun --exec "cwl-runner shrek.cwl passN.yaml" ...
```

(worker nodes will execute job under the control of cwl-runner... panda/pchain will steer the global workflow)

---


- I need to stage files using rucio...
	```
	cwl-runner donkey.cwl passN.yaml
	```
- I need to produce the documentation for this pass...
	```
	cwl-runner fiona.cwl passN.yaml
	```
- I need to get the current status of the production pass...
    ```
	cwl-runner boots.cwl passN.yaml
	```
...


---
