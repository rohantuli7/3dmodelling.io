# 3D Face Modelling

Documentation for the project of 3D face reconstruction. 

# Table of contents

```{tableofcontents}
```

# Project overview

```{figure} /images/code_overview.png
---

name: code_overview
---
Code overview
```

To ensure modularity, portability, and streamlined development, the codebase of our 3D head modeling project has been divided into distinct sections. Each section serves a specific purpose, contributing to the overall efficiency and effectiveness of our computer vision application. The sections are:

## Dockerfiles
Dockerfiles play a crucial role in our 3D head modeling project by providing a standardized and reproducible environment for our code execution. Docker is a containerization platform that allows us to package our application, along with all its dependencies, into a portable container. This means that our code can be run consistently across different systems, eliminating the notorious "it works on my machine" issue. Each library/method used during this research has been developed and tested using these Dockerfiles.

## Containers
Containers are the instances created from our Docker images. These containers encapsulate the entire runtime environment, including libraries, dependencies, and configuration, making them self-sufficient and isolated from the host system. With containers, we can run multiple instances of our 3D head modeling application concurrently without any conflicts. The MICA container (cool_spence) has been used for most of the development.

## Data collection repository (GitHub):
The data collection repository on GitHub contains scripts and codebases which are useful for tasks such as folder creation and landmark annotation during the data collection process. Refer to the [GitHub repository](https://github.com/rohantuli7/emteq_dc_scripts) for further information.

# Libraries
In this project, the following libraries have been used for research purposes:
1. [FLAME](https://github.com/TimoBolkart/TF_FLAME): FLAME is a lightweight and expressive generic head model learned from over 33,000 of accurately aligned 3D scans. FLAME combines a linear identity shape space (trained from head scans of 3800 subjects) with an articulated neck, jaw, and eyeballs, pose-dependent corrective blendshapes, and additional global expression blendshapes 

2. [RingNet](https://github.com/soubhiksanyal/RingNet): Learning to Regress 3D Face Shape and Expression from an Image without 3D Supervision

3. [MICA](https://github.com/Zielon/MICA): Towards Metrical Reconstruction of Human Faces

4. [Flame-fitting](https://github.com/Rubikplayer/flame-fitting): Converting an arbitary scan to FLAME topology

5. [FAN (facial alignment)](https://github.com/1adrianb/face-alignment) : Detecting 2D and 3D landmarks using an accurate face alignment network

6. [DECA](https://github.com/yfeng95/DECA): DECA reconstructs a 3D head model with detailed facial geometry from a single input image. The resulting 3D head model can be easily animated. This library has been used for extracting expression and pose features from an image.

# Important links

1. [3D Face Modelling folder](https://drive.google.com/drive/folders/11ggVeXjfMOr2onn13Cr3I6KXH-cqQk7U?usp=share_link)

2. [Weekly presentations](https://drive.google.com/drive/folders/1FKkPzT_dap9Us4mJon2C1A-4ExyU83ly?usp=share_link)

3. [Data collection files](https://drive.google.com/drive/folders/1mokJA-dQMqjqR14uixTLV0dwtw6hx2Nw?usp=share_link)

4. [Docker images](https://drive.google.com/drive/folders/16td6ucSFobm5EyPJO-w6TFYxCs4RNsaN?usp=share_link)