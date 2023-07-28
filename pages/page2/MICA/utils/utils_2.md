# Video utils

This section describes the video utilities developed during this project. Video utils is located in the ```/MICA/video_utils``` directory and contains two scripts: (i) ```video_helper.py``` and ```mesh_helper.py```.

## Mesh helper
This script contains mesh utility functions which are used to create average vertices of multiple MICA meshes.

1. ```get_meshes(basePath, eye_type)```:
    - Function used to load MICA meshes which are based on the visibility of the eyes
    - Input:
        - ```basePath```: path to meshes
        - ```eye_type```: three distinct options (LEFT, RIGHT or BOTH)
    - Returns:
        - dict(frame_number(int) : mesh(trimesh))

2. ```get_scales(basePath, eye_type)```:
    - Loads numpy scale (scaling factor) files based on the eye region
    - Input: 
        - ```basePath```: path to meshes
        - ```eye_type```: three distinct options (LEFT, RIGHT or BOTH)
    - Returns:
        - scales(numpy)

3. ```get_scales_meshes(meshes, scales)```:
    - Applies scaling factors to the meshes
    - Input:
        - ```meshes```: dict of trimesh meshes and frame number
        - ```scales```: list of scales
    - Returns: list(scaled_meshes(trimesh))

4. ```get_mean_meshes(meshes)```:
    - Averages the meshes based on their vertices
    - Input:
        - ```meshes```: list of Trimesh meshes
    - Returns:
        - average_mesh(Trimesh)

5. ```create_mean_mesh(fileName, basePath = "./demo/batchInput")```:
    - Function to create mean meshes. Saves the meshes at the ```fileName``` folder
    - Input: 
        - ```fileName```: file name of the mesh directory to process
        - ```basePath```: path to base directory of all mesh folders
    - Returns: 
        - None

    
## Video helper
This script contains video utility functions which are used to create average vertices of multiple MICA

1. ```euclid_dist(a, b)```:
    - Euclidean distance between two points
    - Input:
        - ```a```: first point or array
        - ```b```: second point or array
    - Returns
        - Distance(int)

2. ```avg_iris_size(pts)```:
    - Calculates the average iris size
    - Input:
        - ```pts```: left, top, bottom and right 2D coordinates of each eye
    - Returns:
        - Average size (int)


3. ```scaling_factor_func(image, show_output=False, flip=False, RGB=True)```:
    - Calculates the iris distance using mediapipe's face mesh function
    - Input:
        - ```image```: image of a person (2D numpy array)
        - ```show_ouput```: display the image with iris points (default: False)
        - ```flip```: flag to flip image (default: False)
        - ```RGB```: flag to change image channels (default: True)
    - Returns:
        - left iris scaling factor (float)
        - Right iris scaling factor (float)

4. ```get_frames(vidPath)```:
    - Loads and splits video in frames
    - Input:
        - ```vidPath```: path to video
    - Returns
        - frames (numpy array)
        - fileName (str)

5. ```frame_nums(num_frames)```:
    - Function to calculate the 1/4, 1/2 & 3/4 frame indices
    - Input:
        - ```num_frames```: number of frames (float)
    - Returns:
        - 1/4th frame index
        - 1/2th frame index
        - 3/4th frame index

6. ```choose_frames(frames, NUM_SAMPLES = 10)```:
    - Function to choose a defined number of frames randomly
    - Input:
        - ```frames```: all frames (numpy array)
        - ```NUM_SAMPLES```: number of random frames to choose (default: 10)
    - Returns:
        - left eye frames (np array)
        - Both eye frames (np array)
        - Right eye frames (np array)

7. ```save_frames(baseDir, frames, eye_type)```:
    - Function to save frames
    - Input:
        - ```baseDir```: base directory to save frames (str)
        - ```frames```: frames (np array)
        - ```eye_type```: LEFT, RIGHT or BOTH (str)
    - Returns:
        - None