(M1)=
# MICA

MICA is the primary container used for research and development in this project. 

The following analysis and codebases have been developed and executed in this container:

```{figure} /images/MICA_overview.png
---

name: mica_container
---
MICA container overview
```

```{note}
Check the [issues](issues) section before executing the flame-fitting repo.
```
## Libraries
Development in this container can be divided into the following sections:

1. Mesh libraries
    - MICA
    - DECA
    - FLAME reverse fitting
    - FLAME
2. Analysis
    - Data collection
    - Data collection trial
    - Calibration
3. Utils
    - Data loader
    - Video utils
    - Mesh utils

(M3)=
## Processed data loading
While working with this container, load the participant data files from [here](https://drive.google.com/drive/folders/1NPIvkFrtodAK_NFJj6zSKbgrerDwOHTH?usp=share_link).
- Unzip ```emteq_data_collection.gz``` & ```files.gz``` files in the ```/MICA``` directory
```{warning}
Without these files, the data collection analysis will not work and all participant data will have to be loaded seperately. Additionally, ensure the folder structure is followed correctly.

```
