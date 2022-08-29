MOGO Lib

![[Pasted image 20220829134328.png]]

Essential idea... when propagating a track through a volume, we will gain by holding all of the daughter volumes (inclu shapes, materials, transforms, etc...) within a contiguous memory layout... to minimize cache misses.

[Stack Overflow on Coniguous Memory Layout](https://stackoverflow.com/questions/46639023/contiguous-storage-of-polymorphic-types)

Use of std::variant...  plus vectors... plus in place construction.

Possibly only issue would be that vectors can still scatter the data accross the heap.  

