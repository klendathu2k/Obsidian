Added handshake to the panda server when shrek-submit runs, so that we don't freeze up when we have a stale token.  Now, we will be prompted to login and get a new, minty fresh token.   (Implemented on Monday.  Successfully tested on Friday morning when the token expired.)

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

(Time for a rant.  Debugging *documentation* takes a long time, and could have been avoided if the examples on the pchain documentation page *had been tested*.  They do not / cannot run at BNL, because they take as input data sets which have not been defined.)  

Ran into another *fun* issue on Wednesday.  The pileup job was launching before all of the files it required had been produced by the charm and background simulations.  This spontaneously resolved Wednesday morning.  Although I have seen at least one more instance of this since then.  Once I have a production workflow setup and running at scale... can stress test to maybe identify.   But may well just be teething pains that have been fixed?

Now, back to the issue with wildcard files...  I cannot actually unpack the tarballs that are handed to me.

I am using the --forceStaged and --forceStagedSecondary options to prun.  I expect that the tarballs will be in the working directory on the node.  They are not.  I see symbolic links instead.  

No matter.  Tar should be able to follow the link, correct?  WRONG!  The link appears to be circular.  See [this github gist...](https://gist.github.com/klendathu2k/d4dcbac7d6f219777006b09a22ac8bd1).  Emailing Tadashi... 

Considering  a workaround for this.

Defining outputs with a wildcard is required.  Not because the *number* of outputs is unknown, but because the *name* of the outputs is unknown.  Perhaps the solution here is to just pack the file up in a tarball myself, and unpack at the next stage of input.



