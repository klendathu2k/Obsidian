# geant4star status
---
![[Pasted image 20220316081737.png]]
 
---
## Integration
- Made two Pull Requests to move code which does not depend on g4star 
	-  [Closed PR#305](https://github.com/star-bnl/star-sw/pull/305)
	-  [Open PR#308](https://github.com/star-bnl/star-sw/pull/308)
- Large PR draft to pull in geant4maker code and related changes
	- Draft [PR#311](https://github.com/star-bnl/star-sw/pull/311)
	- Early comments / review requested

---

![[Pasted image 20220316084925.png]]

---

- Checks known to fail (must adjust environment before compile)
	 - root 6.24 compiled locally w/ debug
	 - geant3 vmc compiled locally w/ sensitive detector fix
 - Code is compiled in EVAL (will release following this meeing)

---

 To build
 - $ git clone https://github.com/klendathu2k/star-sw-1
 - $ git checkout star-main-geant4star
 - $ source StRoot/StGeant4Maker/etc/setup
 - $ source StRoot/StGeant4Maker/etc/build
 - Make coffee / drink coffee / repeat

---

 To run (from eval)
 - $ starver eval
 - $ source $STAR/setup
 - $ ln -s StRoot/StGeant4Maker/tests .
 - $ ln -s StRoot/StGeant4Maker/macros .
 (Just the following for a local build...)
 - $ geant4star -q -b --geant321 --application:engine=multi tests/unit_test_tpc_hits.C



