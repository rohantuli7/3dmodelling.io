# Dockerfiles & images

## Prerequisites
1. docker: for non-GPU codebase execution
2. nvidia-docker: for GPU acceleration

(df1)=
## Dockerfile structure
Each 3D modeling library (FLAME, MICA, etc.) uses a different Python version for execution; thus, it is recommended not to create Python environments in the Dockerfile, and it would be easier to create and maintain them inside the container.

```{note}
To provide GPU support to these docker images, nvidia-docker is required to be installed on the machine
```

The following code remains consistent in each dockerfile: 

1. Pulling the Ubuntu nvidia-cuda enabled image. This step is crucial in determining the compatibility of the CUDA & Ubuntu version required by the deep learning libraries.
```
FROM nvidia/cuda:11.3.0-cudnn8-devel-ubuntu18.04
```

2. Installing the necessary binaries for Linux
```
RUN apt-get update && apt-get install -y --no-install-recommends \
         build-essential \
         cmake \
         git \
         curl \
         vim \
         ca-certificates \
         libboost-all-dev \
         python-qt4 \
         libgl1 \
         libjpeg-dev \
         libpng-dev \
         wget \
         unzip &&\
     rm -rf /var/lib/apt/lists/*
```

3. Installing and initialising miniconda 
```
RUN curl -o ~/miniconda.sh -O  https://repo.anaconda.com/miniconda/Miniconda3-py39_23.1.0-1-Linux-x86_64.sh  && \
     chmod +x ~/miniconda.sh && \
     ~/miniconda.sh -b -p /opt/conda && \
     rm ~/miniconda.sh

RUN opt/conda/bin/conda init
ENV PATH /opt/conda/bin:$PATH

RUN conda config --set always_yes yes --set changeps1 no && conda update -q conda 
```

4. Copying the working directory into the Docker image

```
WORKDIR /MICA
COPY . .
```

5. Specifying the port number
```
EXPOSE 9999
```

## Docker images

The following Docker images have been used for this research

1. MICA
```
FROM nvidia/cuda:11.3.0-cudnn8-devel-ubuntu18.04
```

2. FLAME, face-alignment, & flame-fitting
```{note}
flame-fitting codebase does not need a GPU or cuda libraries for execution.
```

```
FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu18.04
```

3. RingNet
```{note}
RingNet has been developed using Python 2.7
```
```
FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04
```

## Docker commands
1. Building the dockerfile
After the dockerfile is written, the following command is used to build it into an image:
```{note}
The -t tag is required to give the image a name manually; otherwise, it automatically assigns one.
```

```
docker build -t <image-name> .
```

2. Creating a container
To create a container for a given image, the following command is used:

```{note}
The -p tag is required to map the Docker port onto the local machine.

The -it tag allows interactive development.
```

2.1 Non GPU execution:
```
docker run -p 3000:3000 <image-name>
```

2.2 GPU execution:
```
nvidia-docker run -it -p 9999:9999 <image-name>
```

2.3 VScode:

To facilitate smooth development inside the container, the Docker VScode extension has been used, which allows the VScode environment to be attached to the container. The container can also begin execution, start, and stop through this extension.