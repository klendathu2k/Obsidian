 sPHENIX Handy Remote Execution Coordinator  (SHREK) *working title*
![[Pasted image 20220323093933.png|400]]

---

![SHREK](https://lh4.googleusercontent.com/G5w4P1uwUYpU-ObA8T3fDdm27jEm66IxTQ-sHTB8_LGZQbZpQK4xGBMeMpDTHxCBIPt9_vnBkuWdjTYcaTGBhjLEMC4giqNX_YLv9d5RR6G4mJgOiw9O9e1q4l-GcA1dZMVp1Nl-) 

---

CWL --> [Common Workflow Language](https://www.commonwl.org/)

---

Documentation is the language specification / Tutorials are far too trivial

![|400](https://lh3.googleusercontent.com/ZRFfya9MXZBd8nmAErP_oei8r1uFAGE7Yxkl1dFqvNbqw3GP74_BAyxc4WXeAnbMmDuSiR28UE68p__IGIgirtB4wRdWBPOAN1-nz_UHoGuzY9pmwnRUQkOnLmk_EYXcvSX42vt7)

---

Important to note:
- CWL is used by *panda* to run *prun tasks* on the remote PanDA server

- all production codes must be wrapped by a script which 
	- sets up the environment
	- manages job parameters (such as run number, sequence/RNG number, etc...), some of which are generated per job by PanDA

---

Also important to note:
- Having used SUMS for the better part of two decades now... some of my normal expectations are inverted...

With SUMS, you must be explicit about staging artifacts to the remote system (scripts, macros, etc...)
With PanDA, the files in your CWD are recurssively staged (up to a size limit which can be changed)

---

 Framework for Remote Execution Development (FRED) *alternate title...*
![[Pasted image 20220323094628.png]]

---

Networkable Execution Modeling Objects (NEMO) *... stretching things a bit...*
![[Pasted image 20220323095228.png|400]]

---





