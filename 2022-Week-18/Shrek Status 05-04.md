# SHREK Status 
## May The 4th
*(be with you)*

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
		- Tasks which require no input run to completion

---

- I need to know where to get started with staging data sets / rucio

---




