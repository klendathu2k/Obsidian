[Use valgrind / massif](https://stackoverflow.com/questions/131303/how-can-i-measure-the-actual-memory-usage-of-an-application-or-process) to profile the memory usage.

- n.b. I may have issues b/c geant3 may be loaded by default... and when it loads, it grabs memory... (or does it?  does vmc G3 actually allocate memory dynamically on heap, or is it static memory ala starsim? ... and come to think of it... starsim is dynamic at run time, so???)


