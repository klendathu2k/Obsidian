SHREK 

Setup the sPHENIX heavy flavor workflow to run charm (signal) + minbias (background) feeding those two inputs into the pileup job.  Required a small workaround, hardcoding the location of the HepMC input files used for event generation on the minbias sample b/c (1) do not yet have ability to create datasets via rucio and (2) unable to stage large (2GB+) files (b/c soft limit for PanDA / hard limit on home directory quotas...)

Spent too much time fighting with PanDA credentials.... (logged in with jwebb instead of jwebb2... and PanDA doesn't forget your username when you log out... and doesn't give you the option to log in as a different user...)  Ended up clearing cookies, cache, etc...

]


