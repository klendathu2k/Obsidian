Added handshake to the panda server when shrek-submit runs, so that we don't freeze up when we have a stale token.  Now, we will be prompted to login and get a new, minty fresh token.  

Tadashi made a server side fix over the weekend.  So issues I was having all day on Friday just magically disappeared. 

Got clarifiction on how wildcards work.  There is an extra step (documented under prun, but not under pchain...) that wildcard matched outputs get packed into a gzipped tarball.  But more on this later...

Got clarification that nFilesPerJob *defaults to 50* if it is unspecified.     There was a mistake in my code that was leaving this unspecified for the primary (but not secondary) data sets.  Plus.... I happen to think a default of 1 file per job is the only sensible default value here...  but regardless...  Fixed the mistake in my code, and now I have the expected number of pileup jobs lauched against the charm generation and background generation jobs (1 pileup job for each charm job, with N background jobs fed in).

But ... time for a rant here...

pchain documentation missed something.  All of its examples which specify secondary data sets had a problem:

```
 premix:
 run: prun
 ...
 opt_args:
 default: "--outputs klm.root --secondaryDSs %IN2:2:%{DS1}"
 ...
 ```

