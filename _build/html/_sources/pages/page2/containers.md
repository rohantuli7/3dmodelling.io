# Containers

```{figure} /images/containers.png
---

name: containers
---
Containers used in this project
```

```{note}
Also see the [data loading section](M3) when using the MICA container.
```

<!-- ![containers](/images/containers.png) -->

Containers have been employed as a foundational component for the development of code in our 3D head modeling project. The following containers have been used:

1. ```MICA``` (cool_spence)

2. ```flame-fitting``` (suspicious_morse)

3. ```RingNet``` (silly_leavitt)

Each of these containers has been initialized and set up to run respective libraries in them.

The zipped container images are uploaded on Google Drive [here](https://drive.google.com/drive/folders/16td6ucSFobm5EyPJO-w6TFYxCs4RNsaN?usp=share_link).

## Container information
- The ```MICA``` container is primarily used for all development
- ```flame-fitting``` deals with converting arbitrary head models (H2, EM3D, etc.) into FLAME topology and has also been extended to fitting OCOSense eyeglasses on the converted FLAME mesh (incomplete).
- The ```RingNet``` container implements the RingNet repository. However, it is recommended to avoid using this container for development as the RingNet library has been developed using Python 2.7.