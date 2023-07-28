# Mesh utils

This section describes the mesh utilities developed during this project. This library has been primarily used for in the ```data collection analysis``` stage.
```{note}
Location: `/MICA/src/utils/mesh_utils.py`
```

## Registration and calibration


1. ```transform_mesh(known_lmks, arb_lmks, arb_mesh)```:
    - Uses procrustes to align one mesh with another
    - Input:
        - ```known_lmks```: target alignment landmarks (np array)
        - ```arb_lmks```: arbitary landmarks (np array)
        - ```arb_mesh```: mesh to transform (Trimesh)
    - Returns:
        - ```transformedMesh```: transformed mesh
        - ```trans_lmks```: transformed landmarks

2. ```detect_outliers_iqr(data, factor=1.5)```:
    - Function to detect outliers using IQR
    - Input:
        - ```data```: array with distances (numpy array)
        - ```factor```: factor for outlier detection (defaut: 1.5, dtype=int)
    - Returns:
        - Bool mask (numpy bool array)
(mu3)=
3. ```calib_MICA_h2(H2Lmks, MICAMeshes, MICALmks)```:
    - Calibrating MICA meshes with H2
    - Input:
        - ```H2Lmks```: H2 landmarks (numpy array)
        - ```MICAMeshes```: MICA meshes (dict(expression(str):mesh(trimesh)))
        - ```MICALmks```: MICA landmarks (dict(expression(str):landmarks(np array)))
    - Returns:
        - ```m```: transformed meshes (dict(expression(str):mesh(trimesh)))
        - ```l```: transformed landmarks (dict(expression(str):landmarks(np array)))

## Mesh analysis

4. ```show_dist(mesh1, mesh2, color_map="cool")```:
    - Heatmap which displays difference between two meshes
    - Input:
        - ```mesh1```: mesh to compare with other mesh (Trimesh)
        - ```mesh2```: other mesh (Trimesh)
        - ```color_map```: color map for heatmap (default: "cool", dtype: str)
    - Returns:
        - None
(mu5)=
5. ```get_diff_mesh(mesh1, mesh2, method="clip", clip_min=0.1, color_map="jet")```:
    - Function to get differences between two meshes omiting outlier points
    - Input:
        - ```mesh1```: mesh to compare with other mesh (Trimesh)
        - ```mesh2```: other mesh (Trimesh)
        - ```method```: outlier detection method (default: "clip", options: "clip" or "iqr", dtype=str)
        - ```clip_min```: minimum clip range (only used when method="clip", default: 0.1, dtype=str)
        - ```color_map```: color map (default: "jet", dtype=str)
    - Returns:
        - ```diff_mesh```: Mesh with heatmap face colours
        - Non outlier distances array

6. ```show_diff_mesh(diff_mesh, dsts)```:
    - Function to display differences between two meshes
    - Input:
        - ```diff_mesh```: mesh generated using [```get_diff_mesh()```](mu5)
        - ```dsts```: Non outlier distances array calculated using [```get_diff_mesh()```](mu5)
    - Returns:
        - None

7. ```show_lmks(rows, cols, meshes, lmks)```:
    - Function to show meshes and their respective landmarks
    - Input:
        - ```rows```: number of rows of mesh plots(int)
        - ```cols```: number of columnrs of mesh plots (int)
        - ```meshes```: meshes dict (expression(str):mesh(Trimesh))
        - ```lmks```: landmark dict (expression(str):mesh(Trimesh))
    - Returns:
        - None

(mu8)=
8. ```get_mesh_diff_data(mesh_data, mesh)```:
    - Main function to call [```get_diff_mesh()```](mu5) for multiple meshes
    - Input:
        - ```mesh_data```: meshes dict (expression(str):mesh(Trimesh))
        - ```mesh```: Target mesh (Trimesh)
    - Returns:
        - ```d```: difference meshes and distances (dict(meshes:diff_meshes(dict), dsts:dsts)) 

9. ```show_all_mesh_diff(rows, cols, dsts, meshes)```:
    - Function to show heatmaps of all meshes for different expressions
    - Input:
        - ```rows```: number of rows of mesh plots(int)
        - ```cols```: number of columnrs of mesh plots (int)
        - ```dsts```: distances dict (expression(str):mesh(Trimesh)) from [```get_diff_mesh()```](mu8)
        - ```meshes```: meshes dict (expression(str):mesh(Trimesh)) from [```get_diff_mesh()```](mu8)
    - Returns:
        - None

## Glasses fitting
(mu10)=
10. ```get_trans_glasses(mesh, template_mesh, glasses, idxs, isScaled)```:
    - Transformed and registered glasses
    - Input:
        - ```mesh```: head mesh (Trimesh)
        - ```template_mesh```: template head mesh (Trimesh)
        - ```glasses```: OCOsense eyeglasses (Trimesh)
        - ```isScaled```: flag to scale glasses (bool)
    Returns
        - ```new_glasses```: registered glasses (Trimesh)

(mu11)=
11. ```get_regs_glasses(mesh, glasses, calib_mesh, idxs)```:
    - Creates scaled and unscaled glasses - Calling function for [get_trans_glasses()](mu10)
    - Input:
        - ```mesh```: head mesh (Trimesh)
        - ```glasses```: OCOsense eyeglasses (Trimesh)
        - ```calib_mesh```: calibrated head mesh obtained using [calib_MICA_h2()](mu3)
        - ```idxs```: reference indices for fitting
    - Returns
        - ```d```: dict with scaled and unscaled glasses


12. ```display_glass_intersection(mesh, glasses_data, expName)```:
    - Displays intersected volume of glasses with mesh
    - Input:
        - ```mesh```: head mesh (Trimesh)
        - ```glasses_data```: dict with scaled and unscaled glasses obtained from [get_regs_glasses()](mu11)
        - ```expName```: expression name (str)
    - Returns:
        - None

13. ```display_mesh_glasses(mesh, glasses_data, expName)```:
    - Displays head mesh with fitted glasses
    - Input:
        - ```mesh```: head mesh (Trimesh)
        - ```glasses_data```: dict with scaled and unscaled glasses obtained from [get_regs_glasses()](mu11)
        - ```expName```: expression name (str)
    - Returns:
        - None


## Shape code analysis

14. ```show_ptwise_diff(frame_ids, target_code)```
    - Heatmap of shape identities across all frames
    - Input:
        - ```frame_ids```: shapecode identities (numpy array)
        - ```target_code```: target shape code (numpy array)
    - Returns
        - None

15. ```show_frame_boxplots(frame_ids)```
    - Displays boxplots for shapecode vector distribution across all frames
    - Input:
        - ```frame_ids```: shapecode identities (numpy array)
    - Returns:
        - None