Added handshake to the panda server when shrek-submit runs, so that we don't freeze up when we have a stale token.  Now, we will be prompted to login and get a new, minty fresh token.  

Tadashi made a server side fix over the weekend.  So issues I was having all day on Friday just magically disappeared. 

Got clarifiction on how wildcards work.  There is an extra step (documented under prun, but not under pchain...) that wildcard matched outputs get packed into a gzipped tarball.  But more on this later...

Got clarification that nFilesPerJob *defaults to 50* if it is unspecified.     There was a mistake in my code that was leaving this unspecified for the primary (but not secondary) data sets.  Plus.... I happen to think a default of 1 file per job is the only sensible default value here...  but regardless...  Fixed the mistake in my code, and now I have the expected number of pileup jobs lauched against the charm generation and background generation jobs (1 pileup job for each charm job, with N background jobs fed in).

But... secondary file lists were empty.  Why?  Because the pchain documentation was wrong.    All of its examples which specify secondary data sets had a problem:

```
 premix:
 run: prun
 ...
 opt_args:
 default: "--outputs klm.root --secondaryDSs %IN2:2:%{DS1}"
 ...
 ```

"%IN2"  should have been "IN2".  The "%" token is used by PanDA to match where the reference IN2 for the dataset should be substituted.  Tadashi has corrected this mistake. 

(Time for a rant.  Debugging *documentation* takes a long time, and could have been avoided if the examples on the pchain documentation page *had been tested at BNL*.  The one which uses the secondary data sets *do not run at BNL* because *they rely on data sets that do not exist at BNL*, so I could not test them properly myself. )



Ran into another *fun* issue on Wednesday.  The pileup job was launching before all of the files it required had been produced by the charm and background simulations.  This spontaneously resolved Wednesday morning.  Although I have seen at least one more instance of this since then.  Once I have a production workflow setup and running at scale... can stress test to maybe identify.   But may well just be teething pains.



