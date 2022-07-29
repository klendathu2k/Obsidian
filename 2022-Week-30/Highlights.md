STAR StEvent / Forward Calorimetry
- Discussed with Akio how to save the ID truth information he wants... settled on a vector of std::pair<int, float> containing the ID truth of each track which contributes to the hit and the total energy deposited by that track.  (Each track is the parent of an EM/had shower.)  Found the issue with his implementation (needed to declare both the pair and the vector in the ROOT linkdef file.)  Recommended he make the pull request.
- PR discussion about whether a set or map would be better optimized.  When one takes into account the order in which tracks are presented by geant, vector is correct data structure.  (And one should reverse iterate through it).

sPHENIX / SHREK / HF Charm Workflow

- Scaling tests up to 10 HF x 50 background jobs... failing during pass3 track reco ... one job seems to hang and then the production gets stuck.  This does not seem to be consistent, though... so allowing multiple attempts to produce data should (hopefully) resolve the problem.
- Rucio... I have access now (running the setup script on cvmfs, using the sphnxpro credentials)... n.b. the Rucio documentation is inadequate... basically states that the client should work out of the box... but it doesn't even setup a default configuration file in your account.)
- Rucio works (mostly)...   I can access the catalog... I can schedule files for removal (aka "erase").  I can create datasets, containers, and attach one to another.  But I cannot upload or download files, because it appears that that functionality is not setup... either the client isn't setup / configured correctly, or the local server isn't (or both).  Will follow up with Vincent. 
- Looking at the file catalog... I believe there is some misbehavior with PanDA and Rucio.  Intermediate products during a pchain workflow are persistent.  We may not want to save these... as there may be some duplication of files (I currently have a final "merge" task which simply creates a unified data set).


