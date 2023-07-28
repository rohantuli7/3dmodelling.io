# Future work

## Calibration

Calibrating meshes with a token of known size is essential towards converting these meshes from relative co-ordinates to real world co-ordinates. Currently, the meshes generated using videos are calibrated using H2 landmarks. 

The reason for employing such a calibration process lies in its ability to establish a reliable and consistent relationship between the virtual mesh and real-world measurements. Without calibration, the generated meshes would lack accurate scaling information, making it challenging to interpret them in real-world units. By placing a known-size circle on the forehead, the computer vision techniques can analyze the size changes of the circle across frames, allowing for the derivation of precise scaling factors.

```{figure} /images/mesh_scaling.png
---

name: calibration
---
Mesh calibration
```

The above [figure](calibration) describes one potential process which could be used for calibrating FLAME meshes. 
- Placing a circle of known size on the participant's forehead while recording facial expression videos could be used for calibrating the output mesh.
- Computer Vision techniques can be used to calculate the size of the circles across all frames which will be further used to estimate the scaling factor. Using the scaling factors across multiple frames can then be used to scale the output mesh.

## Statistical analysis (Relating to expressions to glasses data)

This project primarily focused on utilizing 2D and 3D vision data to analyze glasses fitting. The OCOSense glasses gathered extensive data through their sensors, offering an opportunity to establish a correlation between vision data and sensor data. This correlation would be highly advantageous in deriving statistical analyses and estimating one type of data (vision or sensors) based on the other. One valuable application of this correlation is using OCOSense data to estimate facial expressions. This capability allows for the generation of synthetic data and provides valuable insights for various purposes.

```{figure} /images/statistical_analysis.png
---
name: statistical_analysis
---
Expression analysis with OCOSense data
```

The above [figure](statistical_analysis) describes the process of correlating OCOSense data with an individual's face video expression data.
- The initial step entails estimating the average shape code from MICA across all frames and obtaining framewise expression and pose codes from DECA. These disentangled features can then be leveraged to generate head models for all frames in a short video. Since the head models are constructed based on these disentangled features, the next step involves building an encoder model. 
- The encoder model takes a set of OCOSense data samples as input and estimates the corresponding disentangled features. By doing so, the encoder model facilitates the derivation of valuable insights from the OCOSense data and its correlation with facial expressions and pose variations in the video frames. Ultimately, this process enables the extraction of meaningful information and relationships between the vision data and sensor data gathered by OCOSense glasses, furthering the understanding of glasses fitting and related applications

## Non neutral expression comparision

In the current approach, the comparison between neutral H2 meshes and MICA meshes is limited to neutral expressions because MICA exclusively produces neutral expression meshes. However, by employing DECA to estimate expressions and poses for all frames, the disentangled features obtained can open up new possibilities for analysis. Specifically, these disentangled features can be utilized to create non-neutral fusion meshes, combining both MICA and DECA features. This innovative approach allows for a more comprehensive and nuanced comparison between the fusion meshes and the H2 meshes, providing valuable insights into the variations and transformations of facial expressions beyond the neutral state. The motivation behind exploring non-neutral fusion meshes lies in the need for a more comprehensive understanding of facial expressions and their variations. 

## Frame and shapecode selection 

In the context of head mesh generation, taking H2 as the target mesh and employing reverse FLAME fitting to estimate disentangled features opens up an intriguing possibility. By analyzing the shape codes across multiple meshes and establishing a relationship with the corresponding videos of an individual, it becomes feasible to derive a more accurate representation of the person's head mesh. Unlike the current mean shape code method, which provides a generalized representation, this approach allows for the estimation or selection of specific shape code values based on multiple videos of the same individual. As a result, the generated head mesh can better capture the unique characteristics and variations of the person's facial structure, leading to a more personalized and realistic representation. 

Additionally, the method can be then used to estimate the shapecode for videos individuals which don't have any high resolution scans (H2).


## Further analysis into range of expressions

In this project, the focus primarily centered on shape disentangled features rather than pose and expression. While shape disentangled features play a crucial role in capturing the structural aspects of a head mesh, the project acknowledges the importance of exploring expression codes further. Expression codes capture the dynamic changes in facial expressions, encompassing a wide array of emotions and movements. By delving deeper into expression codes, the project aims to enhance the realism and expressiveness of the generated head meshes, making them more lifelike and relatable to human emotions. Understanding and refining expression codes will be beneficial.

