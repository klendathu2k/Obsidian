SHREK Status 4/27/2022

- Final design: SHREK acts as an abstraction layer on top of PanDA and (eventually) Rucio
- Users implement a set of job description files (yaml) which fully describe each job in the workflow (inspiration from SUMS)
	- A "job" is a unit of work which takes a set of inputs and transforms them into a set of outputs, utilizing a set of resources (e.g. macros).

---

![SHREK](https://lh4.googleusercontent.com/G5w4P1uwUYpU-ObA8T3fDdm27jEm66IxTQ-sHTB8_LGZQbZpQK4xGBMeMpDTHxCBIPt9_vnBkuWdjTYcaTGBhjLEMC4giqNX_YLv9d5RR6G4mJgOiw9O9e1q4l-GcA1dZMVp1Nl-) 

---

```
#                                        runPass1.yaml
Parameters:                                                               name: Pythia8CharmSimulation                                           build: mdc2.8                                                           comment: |-                                                               Generate Pythia8 Charm Events and run through F4A                     nJobs:   10   # create 10 jobs                                         nEvents: 100  # 100 events per job                                     macro: Fun4All_G4_HF_pp_signal.C                                       flavor: Charm                                                           runnumber: 1234567890                                                                                       
Resources:                                 
  - file: ../MDC2/submit/HF_pp200_signal/pass1/rundir/*                                                                             
OutputDataSets:                                            
  - name: Pythia8CharmG4Hits                                      
    comment: |-                                                  
      Pythia8 events                                               
    filelist:                                                    
       - "required:*.root"                                                                                                                                                                                 
JobCommands: |-                                            
  # Initialize sPHENIX software environment                   
  source /opt/sphenix/core/bin/sphenix_setup.sh ${build}                            
  rn=$( printf "%010d" $runnumber )
  sn=$( printf "%05d"  $shrek_job_index )                                                     
  filename=G4Hits-${flavor}-${rn}-${sn}.root
  
  root.exe -q -b ${macro}\($nEvents,\"${flavor}\",\"${filename}\",\"\",\".\"\)                                                                                                        
```

---

- Users provide a set JobCommands (bash shell)
- Resources (macros, scripts, etc... ) staged into the working directory when the job reaches the worker node
- Parameters exposed as environment variables
- Input/Output data sets used to build the workflow graph, and create the CWL document for PanDA submission

---

SHREK parses the user-provided YAML files to build a *directed (acyclic) graph* 
- nodes are the job descriptions
- edges connect nodes from output to input

---

`shrek/scripts/buildWorkflowGraph.py --png --tag pythia8-charm tests/pythia8-charm-simulation/*.yaml`
![[Pasted image 20220420092749.png|400]]

---

*... demo time ...*

---

STATUS
- Design set and well into implementation
- Schemas defined for user input files
- Unit tests defined (incomplete coverage...)
- Submission directory populates w/ user-defined resources and CWL files
- PanDA does not (yet) validate the CWL

---

*"All problems in computer science can be solved by introducing another layer of abstraction."
"... except the problem of too many abstractions.*

![[Pasted image 20220420092749.png]]