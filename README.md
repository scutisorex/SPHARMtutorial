# Claw SPHARM Tutorial
This is a tutorial for running SPHARM analysis on mammal claws using SPHARM-PDM, implemented in 3DSlicer.

You will need:
1. 3DSlicer: download the most recent stable release from [here](https://download.slicer.org/).
2. A few extensions added to slicer: you will need SPHARM-PDM, SlicerIGT, and ShapePopulationViewer, which you can get through the [Extensions Manager](https://slicer.readthedocs.io/en/latest/user_guide/extensions_manager.html). You will also need the DeCA module, which is not yet available through the extensions manager, but can be downloaded from [Sara Rolfe's GitHub](https://github.com/smrolfe/DeCA). Instructions on installing an extension from a file available [here](https://slicer.readthedocs.io/en/latest/user_guide/extensions_manager.html).
3. Cleaned and downsampled claw models, centered at the origin for ease of use. You can find those [here](LINK_NEEDED).
4. A sense of humor.

### Data and landmarking preparation
1. Drag and drop your six claw models and the landmarking template into 3DSlicer. They will appear in the data module.
2. Click the eye next to each claw model to make sure they're at the origin. They should all end up right on top of each other if the centering is correct: ![figure 1](https://raw.githubusercontent.com/scutisorex/SPHARMtutorial/main/images/Fig%201.png)
3. Right-click on the landmarking template and choose "clone". Repeat until there are 6 copies of the landmarking template. Rename each one with the same name as one of the claw models: ![figure 2](https://raw.githubusercontent.com/scutisorex/SPHARMtutorial/main/images/fig%202.png)

### Place landmarks on claws
1. In the Data module, hide all but one of your specimens by clicking the eyeball next to the model. Hide all the landmark lists except the one corresponding to that specimen.
2. Navigate to the Markups module. Select the landmark list that has the same name as the specimen that is visible. Make sure you select the correct landmark list - it's easy to pick the wrong one and end up with your landmarks under the wrong specimen name! 
3. Expand the submenu entitled "Control Points". You will see that there are four landmarks and they all have names that tell where they go: tip, proximodistal midpoint on the dorsal side, proximal end on the dorsal side, and proximal end on the ventral side. ![figure 3](https://raw.githubusercontent.com/scutisorex/SPHARMtutorial/main/images/fig%203.png)
4. Select the "Place a control point" tool, and hover over the 3D view. You will see that it's ready to place the "tip" landmark. ![figure 4](https://raw.githubusercontent.com/scutisorex/SPHARMtutorial/main/images/fig%204.png)
5. Place it at the extreme distal tip of the claw. If you need to move the model around before you can place the landmark, right-click and it will turn off the tool. When you have the model in the right orientation, select the tool again and place the landmark. Place the remaining three landmarks the same way. ![figure 5](https://raw.githubusercontent.com/scutisorex/SPHARMtutorial/main/images/fig%205.png)
6. Repeat steps 1-5 for all six specimens. If you show everything, it looks like this: ![figure 6](https://raw.githubusercontent.com/scutisorex/SPHARMtutorial/main/images/fig%206.png)
7. Save landmarks as .json files, in a new folder called "lms".

### Align claws using DeCA
1. Open the DeCA module. There are six items to specify for rigid alignment of your claws. 
- for Base model, select one of the models in the directory with the centered claws.
- for Base landmarks, select the corresponding .json landmarks (the ones that go with your Base model).
- for Mesh directory, choose the place where your claw meshes are stored.
- for Landmark directory, choose the "lms" directory you made in the previous section. 
- for Aligned mesh directory, make a new folder called "aligned_models".
- for Aligned landmark directory, make a new folder called "aligned_lms".
2. Click the "Run alignment" button. NB! this will only work if the names of the landmarks and the names of the models are IDENTICAL!
3. Reopen the scene in Slicer. Navigate to your aligned_models directory, and drag and drop all the aligned meshes into Slicer. They should all be nicely aligned but will not be scaled in any way, so you might only see the biggest one. Hide it to see the others: ![figure 7](https://raw.githubusercontent.com/scutisorex/SPHARMtutorial/main/images/fig%207.png).

### Make aligned models into labelmaps
1. Right-click on one of your aligned models and select "Convert model to segmentation node". ![figure 8](https://raw.githubusercontent.com/scutisorex/SPHARMtutorial/main/images/fig%208.png)
2. Right-click on the resulting labelmap (nested under the segmentation node) and select "Export visible segments to binary labelmap". ![figure 9](https://raw.githubusercontent.com/scutisorex/SPHARMtutorial/main/images/fig%209.png)
3. Repeat these steps for all of the models.
4. The automatically generated file names get too long, and will prevent you from saving the labelmaps. Rename them with FMNH_specimen-number_Genus_species.
5. Save the labelmaps to a new directory called "aligned_labelmaps".
6. Close the scene.

### Execute SPHARM analysis 
1. Open the SPHARM ShapeAnalysisModule. For Input directory, choose the directory with the labelmaps you made in the previous step. For Output directory, make a new folder called "SPHARMoutput".
2. Under Post Processed Segmentation, change all three values to 0.2.
3. Under Generate Mesh Parameters, set number of iterations to 1000.
4. Leave the rest of the settings as-is for the time being. Click Run ShapeAnalysisModule. It takes kind of a long time so be patient! ![figure 10](https://raw.githubusercontent.com/scutisorex/SPHARMtutorial/main/images/fig%2010.png)

### Visualize results in ShapePopulationViewer
1. Navigate to the ShapePopulationViewer module. Click "add .vtk files".