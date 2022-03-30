CWL is *annoying as frell* b/c you must be explict about everything.  It starts up with an *empty* environment, and setting environment variables has to be done variable-by-variable in **both** the CWL file and the supporting YAML inputs file.  So we need to wrap individial pieces of workflow in *shell scripts*, which either need to be in the system path (not happening) or in a docker container (again a pain in the assembler) or we go through the following hoops to stage and execute the script 

Beware:
- emacs likes to put \\t in places but CWL must be \\t free

- [Howto stage and run a shell script](https://github.com/common-workflow-language/user_guide/issues/158)

The problem is this... I want to use a shell script to wrap a root macro.  But the root macro is a file dependence which needs to be staged as well.  

How do I stage files *that are not known to CWL?*
- [Howto stage secondary files](https://cwl.discourse.group/t/how-to-stage-secondary-files-for-basecommand/130)

Create files at runtime
- [HOWTO](https://www.commonwl.org/user_guide/14-runtime/index.html)

Unit tests for CWL
- [CWL tests](https://github.com/common-workflow-language/cwltool/tree/main/tests)

MIscellaneous
- [Best Practices](http://www.commonwl.org/user_guide/rec-practices/)

- [CWL Tools / Ecosystem](https://www.commonwl.org/tools/)
	- [Janis Transpiler](https://github.com/PMCC-BioinformaticsCore/janis)
	- [scriptcwl python driver](https://github.com/NLeSC/scriptcwl)