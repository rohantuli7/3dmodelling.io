# Utils

This section describes the data loader utility functions developed during this project for code modularisation and encapsulation. 

(dl1)=
## Data loader

- ```MeshData``` class is used to load and process all the data collected during the data collection process. This class primarily deals with the following:
    1. Loading H2 scans and their landmarks
    2. Loading videos of different expressions and generating MICA data (shapecode, meshes and landmarks)
    3. Calibrate MICA meshes with H2 landmarks
    4. Extracting framewise shape (MICA), expression (DECA) and pose (DECA) disentangled features
    5. Creating FLAME models using the disentangled features extracted from video frames
    6. Converting H2 meshes into FLAME topology (FLAME reverse fitting) and estimating the target disentangled features

- This class is used for data creation as well as data loading.

### Class attributes
This class consists of the following attributes:
1. H2
    - ```H2Meshes (dict - expression(str) : mesh(trimesh))```: original H2 meshes for different expressions
    - ```H2Lmks (dict - expression(str) : lmks(np array))``` : H2 landmarks
    - ```H2Sliced (dict - expression(str) : mesh(trimesh))```: sliced H2 meshes

2. MICA data
    - ```MICAMeshes (dict - expression(str) : mesh(trimesh))```: MICA meshes for different expressions
    - ```MICALmks (dict - expression(str) : lmks(np array))```: MICA landmarks
    - ```MICAID (dict - expression(str) : shapecode(np))```: MICA shape identity

3. H2FLAME data
    - ```H2FLAME (dict - expression(str) : mesh(trimesh))```: H2FLAME meshes
    - ```H2FLAMELmks (dict - expression(str) : lmks(np))```: H2FLAME landmarks

4. MICA calibrated
    - ```MICACalib (dict - expression(str) : mesh(trimesh))```: MICA calibrated mesh with H2 lmks
    - ```MICACalibLmks (dict - expression(str) : lmks(np))``` MICA calibrated mesh with H2 lmks

5. All Frames MICA data
    - ```AFMICAMeshes (dict - expression(str) : (frames(str) : mesh(trimesh))```: MICA meshes for different expressions with all frames
    - ```AFMICALmks (dict - expression(str) : (frames(str) : lmks(np))```: MICA landmarks for different expressions with all frames
    - ```AFMICAId (dict - expression(str) : (frames(str) : shapecode(np))```: MICA shape identity

6. DECA expression and poses
    - ```DECAExps (dict - expression(str) : (frames(str) : exp(np array)))``` : DECA expressions for different frames
    - ```DECAPoses (dict - expression(str) : (frames(str) : exp(np array)))```: DECA poses for different frames

### Class paths
The following paths are important for loading and saving data for each participant:
- ```basePath (str):``` base directory path
- ```scansPath (str):``` H2 scans
- ```ocoDataPath (str):``` path for reading & forced_expression videos
- ```landmarksPath (str):``` H2 meshes manually annotated landmarks
- ```MICAPath (str):``` MICA meshes
- ```FLAMEPath (str):``` Reverse FLAME fitted H2 meshes
- ```MICAAllFrames (str):``` path to MICA all frames data

### Methods

#### General functions

1. ```__init__(self, basePath, isLoad=False)```:
    - Initialization function. Calls all creation and loading functions during object creation
    - Input:
        - ```basePath(str)```: path to participant folder
        - ```isLoad(bool)```: flag to load or create participant data

2. ```check_yaml(self)```:
    - Creates a YAML log file for every participant 
    - Input & Returns: None

3. ```update_yaml(self, id)```:
    - Updates YAML log file for a given participant id
    - Input:
        - ```id```: participant id
    - Returns: 
        - None

#### H2

4. ```load_H2_data(self)```:
    - Loads H2 meshes and landmarks from ```self.scansPath``` directory
    - Input & Returns: None

#### MICA

5. ```create_MICA_meshes(self)```:
    - Creates mean MICA meshes, landmarks and shapecode for all videos present in the ```self.videosPath``` directory
    - Input & Returns: None

6. ```load_MICA_data(self)```:
    - Loads mean MICA meshes, landmarks and shapecode present in the ```self.MICAPath``` directory
    - Input & Returns: None

#### H2_FLAME

7. ```create_H2_FLAME(self)```:
    - Creates H2_FLAME meshes (FLAME topology H2 meshes) for all scans present in the ```self.scansPath``` directory
    - Input & Returns: None

8. ```load_H2FLAME(self)```:
    - Loads mean H2_FLAME meshes, landmarks and shapecodes present in the ```self.FLAMEPath``` & ```self.landmarksPath``` directory
    - Input & Returns: None

#### MICA calibrated

9. ```MICA_calib(self)```:
    - Calibrates MICA meshes using the H2 and MICA landmarks
    - Input & Returns: None

#### All frames processing

##### MICA - shape feature code

10. ```create_MICA_AF(self)```:
    - Creates MICA meshes, landmarks and shapecode for all frames of all videos present in the ```self.videosPath``` directory
    - Input & Returns: None

11. ```load_AF_MICA_data(self)```:
    - Loads MICA meshes, landmarks and shapecode for all frames of all videos present in the ```self.AllFramesPath``` directory
    - Input & Returns: None

##### DECA - expression and pose features

12. ```extract_DECA_exp(self)```:
    - Extracts expression and pose parameters using DECA for all frames of all videos present in the ```self.videosPath``` directory
    - Input and Returns: None

13. ```load_exp_pose(self)```:
    - Loads expression & pose for all frames of all videos present in the ```self.AllFramesPath``` directory
    - Input and Returns: None

##### FLAME (Head mesh creation):

14. ```create_exp_meshes```:
    - FLAME function to create head meshes using the shape (MICA), expression (DECA) and pose (DECA) parameters
    - Input and Returns: None

<!-- Also mention about participants.py -->

