Setup root6 evironment... 9/27/2022

cat /cvmfs/star.sdcc.bnl.gov/star-spack/README.md

```
$ setup 64b
$ source /cvmfs/star.sdcc.bnl.gov/star-spack/setup.csh
$ spack env list
==> 10 environments
    star-x86-geant  star-x86-loose  star-x86-root5  star-x86-root6  star-x86-root624  star-x86_64-geant  star-x86_64-loose  star-x86_64-root5  star-x86_64-root6  

$  spack load star-env-root6 target=x86_64
==> Error: Spec 'star-env-root6 arch=linux-None-x86_64' matches no installed packages.
```

Okay... looking at spack documentation... suspect we should do the following instead...

```
$ spack env activate star-x86_64-root6 
```

Seems legit... no error is thrown on this.    But... (even if I switch over to bash...)

```
$ echo $ROOTSYS
/cvmfs/star.sdcc.bnl.gov/ROOT/5.12.00/.sl73_x8664_gcc485/rootdeb
```

Environment does not seem to be set correctly at all.  

-- 

