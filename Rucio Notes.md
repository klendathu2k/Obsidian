## Rucio Notes

[Read the Rucio Paper](https://link.springer.com/article/10.1007/s41781-019-0026-3)

[Even more papers](https://inspirehep.net/literature?sort=mostrecent&size=25&page=1&q=rucio)

### [Files, Datasets, Containers](https://rucio.cern.ch/documentation/file_dataset_container)

- Files are grouped into datasets
- Datasets are grouped into containers
- Containers can be grouped into containers...
- Data IDentifier (DID) represents any set of files, datasets or containers.

DID refers to a single file, dataset or container

A DID consists of a *scoper* and a *name*.

Accounts have RO access to all scopes.   Accounts have write access only to their own scope.  (By default).

If a dataset or container is *open*, content can be added to it.

Once *closed* the dataset or container *stays closed*... they cannot be reopened.  (They can be repaired if something is *LOST*).

... but "reopen" command exists... for priveleged users?  

LFN -- logical file name
PFN -- physical file name (associated w/ storage???)




### [Rucio Storage Elements](https://rucio.cern.ch/documentation/rucio_storage_element)

RSE == Rucio Storage Element... the smallest unit of storage space... logical abstraction...  unique ID plus metadata....

### [Meta Data Attributes](https://rucio.cern.ch/documentation/metadata_attributes)

Looks like physics-related meta data can be attached to datasets and files...

Probably useful from a production perspective... to attach 



### [Replication Management](https://rucio.cern.ch/documentation/replica_management)
