[[SHREK]]

Implemented code to convert from a flat set of yaml files, each describing a single job in a workflow with its inputs and outputs, into a CWL document suitable for submission through PanDA.

Setup a test rig for the workflow, based on the "more complicated pchain" example --  [more complicated workflow](https://panda-wms.readthedocs.io/en/latest/client/pchain.html#more-complicated-chain) 

The output is about 90% of the way there...

Still remaining:  
- Need to make sure I have the name of the input dataset, vs the name of the variables which hold the name of the input datasets, sorted properly.
- Currently the output of each step is explicitly named in the yaml files, rather than applying the stepname/varname convention.
- Should verify that I can specify defaults in the inputs block, rather than supply values through an input file.

STAR

Interacting with two users for simulations requests... Petr Chaloupka wants to restrict decays of particles to w/in the TPC volume... supported through the user decay setting... but is a uniform decay...  will perform his analysis in radial slices instead...

DIptanil Roy is proceeding to the 2015 pp simulations... WIll follow up next round of questions on Monday.

geant4star first round of comments from reviewers... 

TODO:  Split up the PR... BFC options seem the lowest hanging fruit here...