# SHREK Status 05/04/2022

---

- [PanDA Simple Chain](https://panda-wms.readthedocs.io/en/latest/client/pchain.html#simple-task-chain)
	- Builds PanDA workflow from [YAML files](https://github.com/klendathu2k/shrek/tree/main/tests/simple-chain)
	- Validates when submitted with `pchain --check`
	- [Runs to completion](https://panda-doma.cern.ch/tasks/?jeditaskid=65575|65574)

---

- [PanDA More Complicated Chain](https://panda-wms.readthedocs.io/en/latest/client/pchain.html#more-complicated-chain)
	- Builds PanDA workflow from [YAML files](https://github.com/klendathu2k/shrek/tree/main/tests/more-complicated-chain)
	- Validates when submitted with `pchain --check`
	- [Fails to complete](https://panda-doma.cern.ch/tasks/?jeditaskid=65555|65557|1651600566|65556)
		- *Input data sets are not defined*
	- Nevertheless, demonstrates that complicated workflows can be properly defined using SHREK. 

---

- I need to know where to get started with staging data sets / rucio
- ... and retrieving data sets

---

sPHENIX HF Simulation Work w/ SHREK

- [Defined by set of YAML files](https://github.com/klendathu2k/shrek/tree/main/tests/pythia8-charm-simulation)
	- Pass1 HF simulation
	- Pass2 merge with prestaged minbias backgrounds
		- May generate these instead?
- Full workflow to follow




