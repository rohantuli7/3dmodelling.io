# Quickstart guide

## Minimum system requirements

This section provides an overview of the system and its purpose. It should include a brief description of the software or hardware being developed or implemented.

Minimum requirements:
1. Hardware Requirements:
    - Processor: Intel i5 - i7 
    - RAM: 8 - 16 GB
    - Storage: > 100 GB
    - Graphics Card: 
        - Testing: GPU with 4 - 8 GB RAM
        - Training: GPU with 20 GB+ RAM
2. Software Requirements:
    - Operating System: MacOS, Linux & Windows
    - Additional Software: docker (essential) & VSCode (essential)

## Installation



### MICA docker image

1. Install docker, nvidia-docker or docker-desktop

    ```{note}
    nvidia-docker is a mandatory installation to enable GPU processing
    ```
2. Download the ```MICA``` image from [google drive](https://drive.google.com/drive/folders/16td6ucSFobm5EyPJO-w6TFYxCs4RNsaN?usp=share_link)

3. It is recommended to attach volumes to your container to enable easy access of data. In any case, data can also be directly loaded into the container. 
    ```{note}
    It is essential that the container which is being used for development is not removed/deleted. **If the container is deleted, all the progress will be lost!**
    ```

4. Create a container from the ```MICA``` image using the following commands:
    ```
    nvidia-docker run <image-name> 
    ```
    
    ```{note}
    The above command will create a container which can be viewed using the `docker ps -a` command
    ```

5. Download the docker VSCode extension. Using this extension (located at the left nav pane), start the container which was created previously. Right click on the container and attach VSCode - this will open a new window which loads the container and allows for development in the chosen environment.

6. Open terminal in the VSCode editor and check if the ```emteq_dc``` environment has been activated. If not, activate it using the following command:
    ```
    conda activate emteq_dc
    ```
    ```{note}
    Use this environment for all code execution. This environment supports all libraries included in the container.
    ```
    ```{note}
    Refer to the [Dockerfile](df1) and [MICA](M1) sections for further information
    ```

#### Data collection analysis

After the above steps have been completed successfully, new participants data can be processed and analysed using the steps given below.

##### Participant data processing
1. To process new participant data, load the participant data into the ```emteq_data_collection``` folder with the right identifier (1, 2, 3, ...).
    ```{note}
    Ensure the data has been correctly uploaded with respect to the file structure and not missing any files.
    ```
2. Move the ```glasses``` folder (and the contents inside it) to the base participant folder directory (example: ```/emteq_data_collection/1```)
3. Processing new partcipant data
    - Open ```participants.py``` script located in ```/MICA/src/dc_analysis``` change the ```PARTICIPANT_IDS``` variable to the identifiers of the participants whose data is to be processed:
        ```{note}
        Example: `PARTICIPANT_IDS = [1, 2, 3]`
        
        Set `isLoad=False` when calling `MeshData()`
        ```
    - Change the directory to the ```cd /src/dc_analysis/notebooks``` directory then execute the ```partcipant.py``` script.
    - To check if all the files are loaded and processed correctly, check the ```data_log.yml``` file in each participant folder. If ```created``` flags for all processes are true, the data has been processed correctly. Additionally, check the terminal for any errors.

    ```{note}
    Refer to the [Data loader](dl1) section for further information
    ```

##### Data collection notebooks
1. Each participant's data has been used for (i) [mesh](ma1) & (ii) [shapecode](ma2) analysis. These notebooks are stored in the ```/MICA/src/dc_analysis/notebooks``` directory
    ```{note}
    Further information can be found in the [analysis](analysis1) section
    ```
2. Each participant will have their own folder in the above mentioned directory consisting of two notebooks
    1. [```mesh_analysis.ipynb```](ma1)
    2. [```shapecode_analysis.ipynb```](ma2)
3. For every new participant, duplicate the participant folder and change the ```PARTICIPANT_ID``` variable in ```mesh_analysis.ipynb``` and ```shapecode_analysis.ipynb``` to the new participant. 

#### Data loader
1. For further analysis, it is recommended to use the data loader class ```MeshData()```. It provides easy retrieval of all data for a particular participant.
    ```{note}
    Refer to the [Data loader](dl1) section for further information
    ```

### Individual library installation

- For each library, follow the steps mentioned in the following links:
    1. [FLAME](https://github.com/TimoBolkart/TF_FLAME)
    2. [DECA](https://github.com/yfeng95/DECA)
    3. [MICA](https://github.com/Zielon/MICA)
    4. [Flame-fitting](https://github.com/Rubikplayer/flame-fitting)
    5. [RingNet](https://github.com/soubhiksanyal/RingNet)

## Glasses fitting
1. The ```flame-fitting``` docker image is created for fitting arbitary meshes into FLAME topology which is further used for fitting OCOSense glasses on the mesh. This method might produce incorrectly results for some meshes (EM3D) and hasn't been tested for other meshes (H2).
2. For glasses fitting on the ```MICA``` mesh, refer to the [glasses fitting](m1_1) functions and the [```mesh_analysis.ipynb```](ma1) notebooks.