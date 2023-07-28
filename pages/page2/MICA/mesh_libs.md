# Head modelling

The MICA container contains the codebases for the following libraries:

## FLAME
- FLAME is the underlying model used by all shape models used in this research. Given a face image and its respective 51 landmarks, FLAME is able to
    1. Disentangle face features into shape, pose, and expression.
    2. Create a 3D head mesh of the individual using the disentangled features
- The authors of FLAME have developed PyTorch and TensorFlow versions of the library. In this container, the PyTorch version has been used. The TensorFlow version has been used separately to create a docker image and test its working.
- In this container, FLAME has been used to create the head mesh of an individual using the disentangled features.

```{figure} /images/FLAME.png
---

name: FLAME_hm
---
FLAME model
```

- The base library is placed in the ```/MICA/FLAME_PyTorch``` directory and used in the ```/MICA/src/dc_analysis/mesh.py``` data loader script.
- This library provides the implementation of ```flamelayer``` which create a FLAME function. This FLAME function is used to create head meshes in ```mesh.py``` using the shape (MICA), expression (DECA) and pose (DECA) parameters. The neck and eyeball parameters are initialised to zeros.
- Installation: FLAME has been installed in the MICA container but for future installation, refer to [FLAME PyTorch](https://github.com/soubhiksanyal/FLAME_PyTorch) or [FLAME TensorFlow](https://github.com/TimoBolkart/TF_FLAME). 

## MICA
- Given MICA's characteristics of being able to represent metrically accurate head meshes, this model is used to extract the shape feature from a given set of landmarks and image/video.
- Method: MICA extracts 2D face landmarks using FAN (internally in its code) which are used for estimating the face shape vector. This method produces a neutral pose & expression mesh and purely focuses on accurate shape code estimation.

```{figure} /images/video_to_mesh.png
---

name: mica_hm
---
Video or image to meshes
```

- Installation: MICA has been installed in the MICA container but for future installation, refer to [this](https://github.com/Zielon/MICA/tree/master). 

- MICA is used in the following configurations
    1. Image to mesh (```demo.py```): 
        - Method: Uses the MICA model to create head meshes 
        ```{note}
        File location: /MICA/demo.py
        ```
        - Input: Image
        - Output: Head model, shape feature vector and 68 face landmarks
        - Usage:
        ```
            python demo.py
        ```
        - The above code processes all the files (images) stored in the ```demo/input/``` folder.

    2. Video to mesh (```vid_recon.py```):
        - Method: Uses the MICA model to estimate the shape code vector of a short video. 60 frames from the video are chosen at random, which are further used to estimate the shape vector of each frame respectively. The estimated shape vectors are averaged and used for the reconstruction of the head mesh
        - Input: Video
        - Output: Head model, shape feature vector and 68 face landmarks
        - Usage:
        ```
            python vid_recon.py -s ./path/to/save/ -v ./path/to/video/example.MOV
        ```

    3. MICA all frames (```mica_frames.py```):
        - Method: Uses the MICA model to estimate the shape code vector of a short video. For each video frame, its frame, shapecode vector, 68 landmarks and head mesh are saved. This method is primarily used for processing video frames and extracting the shapecode from each frame for further analysis. 
        - Input: Video
        - Output: frames, landmarks, shapecode vector and head mesh for each frame in the video
        - Usage:
        ```
            python mica_frames.py -s ./path/to/save/ -v ./path/to/video/example.MOV
        ```

## DECA
- DECA reconstructs a 3D head model with detailed facial geometry from a single input image. This library has been primarily used for extraction of pose and expression from each video frame. 
- Installation: DECA has been installed in the MICA container but for future installation, refer to [this](https://github.com/yfeng95/DECA). 
- Usage: 
    - This library is used in the ```mesh.py``` script
    ```
        MeshData.extract_DECA_exp()
    ```
    - Input: video frames
    - Output: expression, pose, and texture parameters
    - The above function estimates the expression and pose parameters for each frame of a video which is uploaded in the ```emteq data collection``` folder.

## FLAME reverse fitting (or FLAME fitting)
- This library converts an arbitary mesh into FLAME topology. It is used for convert H2 meshes into FLAME topology for comparision and fitting. This library has also been implemented seperately in a container for isolated execution and analysis.

```{figure} /images/scan2mesh.png
---

name: scan2mesh
---
FLAME fitting
```

- It does not use any deep learning libraries and requires the ```chumpy``` and ```psbody.mesh``` library to be installed.
- Installation: FLAME fitting has been installed in the MICA container but for future installation, refer to [this](https://github.com/Rubikplayer/flame-fitting).
- Usage:
    - This library is used in the ```mesh.py``` script.
    ```
        MeshData.create_H2_FLAME()
    ```
    - Input: arbitary mesh (H2)
    - Output: scaled mesh & H2_FLAME mesh
    - The above function converts different expression H2 meshes to FLAME topology.


