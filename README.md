# Claw SPHARM Tutorial
This is a tutorial for running SPHARM analysis on mammal claws using SPHARM-PDM, implemented in 3DSlicer.

You will need:
1. 3DSlicer: download the most recent stable release from [here](https://download.slicer.org/).
2. A few extensions added to slicer: you will need SPHARM-PDM, SlicerIGT, and ShapePopulationViewer, which you can get through the [Extensions Manager](https://slicer.readthedocs.io/en/latest/user_guide/extensions_manager.html). You will also need the DeCA module, which is not yet available through the extensions manager, but can be downloaded from [Sara Rolfe's GitHub](https://github.com/smrolfe/DeCA). Instructions on installing an extension from a file available [here](https://slicer.readthedocs.io/en/latest/user_guide/extensions_manager.html).
3. Cleaned and downsampled claw models, centered at the origin for ease of use. You can find those [here](LINK_NEEDED).
4. A sense of humor.

### Data and landmarking preparation
1. Drag and drop your six claw models and the landmarking template into 3DSlicer. They will appear in the data module.
2. Click the eye next to each claw model to make sure they're at the origin. They should all end up right on top of each other if the centering is correct: IMAGE HERE
3. Right-click on the landmarking template and choose "clone". Repeat until there are 6 copies of the landmarking template. Rename each one with the same name as one of the claw models: IMAGE HERE

### Place landmarks on claws
1. In the Data module, hide all but one of your specimens by clicking the eyeball next to the model. Hide all the landmark lists except the one corresponding to that specimen.
2. Navigate to the Markups module. Select the landmark list that has the same name as the specimen that is visible. Make sure you select the correct landmark list - it's easy to pick the wrong one and end up with your landmarks under the wrong specimen name! 
3. Expand the submenu entitled "Control Points". You will see that there are four landmarks and they all have names that tell where they go: tip, proximodistal midpoint on the dorsal side, proximal end on the dorsal side, and proximal end on the ventral side. IMAGE HERE.
4. Select the "Place a control point" tool, and hover over the 3D view. You will see that it's ready to place the "tip" landmark. IMAGE HERE
5. Place it at the extreme distal tip of the claw. If you need to move the model around before you can place the landmark, right-click and it will turn off the tool. When you have the model in the right orientation, select the tool again and place the landmark. Place the remaining three landmarks the same way. IMAGE HERE
6. Repeat steps 1-5 for all six specimens. If you show everything, it looks like this: IMAGE HERE
7. Save landmarks in a new folder called "lms".

#### Align claws using DeCA
1. Open the DeCA module. There are six items to specify for rigid alignment of your claws. 
