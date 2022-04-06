SHREK Preliminary Design
---

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

```
$ cat run_hfcharm_pass1.yaml

# Specifies a unique name for the job                                  
jobname: g4charm                                                                                                     
# Extra panda flags (such as number of jobs to run)              
extra_panda_args: --nJobs 5                        

# sPHENIX software build level 
build: mdc2.7                                                           

# Job parameters
nevents: 100    # to generate                                            type: Charm     # type of job                                            outfile: TestSubmission                                                 outdir: /sphenix/user/sphnxpro/shrek/pass1/out                         logdir: /sphenix/user/sphnxpro/shrek/pass1/log                         jobdir: /sphenix/u/jwebb2/work/2022/SHREK/MDC2                                       
runnumber: 1234567890                                                   

# Commands to stage files required to run the code 
stagecmd: |-                                                          
  ln -s /sphenix/u/jwebb2/work/2022/SHREK/MDC2/submit/HF_pp200_signal/pass1/rundir/* .                                                   
                                        
# Command block                                                        
commands: |-                                                           
  echo execute a predefined script                                     
  run_hfprod_pass1.sh                                                  
  echo or any arbitrary set of unix commands...                        
  # e.g. root.exe -q -b Fun4All.C                                 
  
# Copy back block                                                       
copyback: |-                                                                                                                             
  ls > ${g4charm_RUNNUM}_${g4charm_SEQNUM}.manifest     

```