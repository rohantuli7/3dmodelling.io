(analysis1)=
# Analysis

In this section, different scripts and code has been developed for [Data collection analysis](analysis2), [Data collection trial analysis](analysis3) and [calibration](analysis4). 

(analysis2)=
## Data collection analysis
For each participant, two python notebooks have been created which are used for mesh and shapecode analysis. This section uses the data loader class (```MeshData()```) in the ```mesh.py``` script. 
```{note}
It is essential that all the relevant data for each participant has been loaded correctly before calling `class MeshData()`
```

- Location: ```/MICA/src/dc_analysis/notebooks```
### Methods
```{note}
All functions below have been imported from `mesh_utils.py` located at `/MICA/src/utils`
```

(ma1)=
#### Mesh analysis
1. Meshes and landmarks (```show_lmks()```):
    - Visual representation of the collected H2 data
    - Input: 
        H2 meshes and H2 landmarks
    - Output: mesh plot with meshes and their respective landmarks
2. H2 neutral vs MICA meshes:
    - Heatmaps of H2 neutral meshes vs MICA
    1. ```get_mesh_diff_data()```:
        - Function to get difference between meshes
        - Input: MICA calibrated meshes and H2 neutral meshes
        - Output: dictionary with meshes and their distances
    2. ```show_all_mesh_diff()```:
        - Function to display mesh heatmaps for different expressions
        - Input: distances & their respective meshes
        - Output: heatmaps showing differences between H2 and MICA

(ma1_3)=
3. Glasses fitting
    - Fitting OCOSense glasses on the face meshes
    1. ```get_regs_glasses()```:
        - Fitting glasses to the mesh
        - Input: template mesh, glasses, MICA meshes, & MICA mesh vertices index
        - Output: scaled and unscaled glasses for respective expression head mesh
    2. ```display_mesh_glasses()```:
        - Displaying fitted glasses
        - Input: Expression mesh, expression scaled and unscaled glasses dict, & expression name
        - Output: Scaled and unscaled glasses fitting for different expressions
    3. ```display_glass_intersection()```:
        - Displaying intersection region and its respective volume
        - Input: Expression mesh, expression scaled and unscaled glasses dict, & expression name
        - Output: 3D intersection volume plot 
4. H2 vs H2_FLAME
    - Mesh heatmap for H2 vs H2FLAME
    1. ```get_diff_mesh()```:
        - Difference between two meshes. Two possible methods, IQR or clipping above a range (Tags: ```iqr``` or ```clip```)
        - Input: mesh1, mesh2, method
        - Output: distance_mesh and distances
    2. ```show_diff_mesh()```:
        - Function to display mesh heatmap
        - Input: distance_mesh and distances (both obtained from ```get_diff_mesh()```)
        - Output: Mesh difference heatmap
5. Expression mesh statistics:
    - Statistical measures between two meshes
    1. ```get_numpy_stats()```:
        - Function to get mean, median, min, max & std of an array:
        - Input: Numpy array or list
        - Output: dict with statistical values
    2. ```get_expression_stats()```:
        - Function to calculate expression stats
        - Input: dict of MICA meshes, & dict of H2 meshes
        - Output: dataframe with statistical results of meshes of different expressions

(ma2)=
#### Shapecode analysis:
1. Shapecode distribution (```show_frame_boxplots()```):
    - Boxplots for different MICA identity (shapecode) index values across multiple frames
    - Input: numpy array of identity values
    - Output: shape identity distribution for different frames
2. Shape code heatmap (```show_ptwise_diff()```):
    - Heatmap of shape identities across all frames
    - Input: numpy array of identity values
    - Output: target shapecode values (obtained from flame-fitting using H2 meshes)

(analysis3)=
## Data collection trial
The previous section [(Data collection analysis)](analysis2) was built on this section thus, only functions not used in the previous section are described here. **This section does not use the ```MeshData()``` data loader class.**

- This section directly refers to the notebooks using the name of the participant.
- Location: ```/MICA/src/notebooks/mesh_analysis/emteq_dct/```

### Methods

#### Shapecode analysis
1. ```transform_mesh()```:
    - Function for aligning meshes using face landmarks. Uses procrustes for alignment
    - Input: target landmarks, arbitary landmarks, & arbitary mesh
    - Output: aligned mesh & aligned landmarks

2. ```get_mesh_data()```:
    - Loads mesh data stored in the following format:
        ```
        ├── basepath
            └── expression1
                └── kpt68.npy
                └── identity.npy
            └── expression2
                └── kpt68.npy
                └── identity.npy
            .
            .   
            └── expression_n
                └── kpt68.npy
                └── identity.npy
        ```
    - Input: basepath and target landmarks
    - Output: dict with meshes and their respective landmarks for all expressions located in the basepath

3. ```show_inter_mica_idx()```
    - Heatmap for comparision between different MICA meshes
    - Input: dict containing MICA meshes and their identity vectors
    - Output: Heatmap

4. ```show_shapecode_diff()```:
    - Barchart displaying the difference between target shapecode (H2) and MICA identities for different expressions
    - Input: MICA meshes dict, & target shapecode
    - Output: Euclidean distances barchart for different expressions

(analysis4)=
## Calibration
This section describes functions used for calibrating a mesh using a token of known size. The code in this section is incomplete and needs to be further worked upon. Some of the code has been used from the ```MICA utils library```.

- Location: ```/MICA/src/notebooks/calibration/3D_to_2D.ipynb```

### Methods

1. ```dist()```:
    - Euclidean distace between two points
    - Input: Points p1 & p2,
    - Output: Euclidean distance

2. ```get_frames()```:
    - Converts a video into frames and estimates face landmarks
    - Input: video 
    - Output: frames and their respective face landmarks

3. ```get_center_frame()```:
    - For a given set of face landmarks obtained from frames of a video, the central or front most frame is calculated (assuming the smallest distance between the fixed landmark indices)
    - Input: landmarks
    - Output: frame index

4. ```detect_circle()```:
    - Detects a token (blue circular dot) on the forehead of an individual. This function assumes the colour and shape of the token to be fixed.
    - Input: image, landmarks, frame_number and option to display output
    - Output: dict with radius, diameter and center of the circle


