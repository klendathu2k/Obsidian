STAR StEvent / Forward Calorimetry
- Discussed with Akio how to save the ID truth information he wants... settled on a vector of std::pair<int, float> containing the ID truth of each track which contributes to the hit and the total energy deposited by that track.  (Each track is the parent of an EM/had shower.)  Found the issue with his implementation (needed to declare both the pair and the vector in the ROOT linkdef file.)  Recommended he make the pull request.
- PR discussion about whether a set or map would be better optimized.  When one takes into account the order in which tracks are presented by geant, vector is correct data structure.  (And one should reverse iterate through it).

sPHENIX / SHREK / HF Charm Workflow

Scaling: 2 jobs @ 10 events