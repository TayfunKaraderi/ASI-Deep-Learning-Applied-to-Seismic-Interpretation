# MSc-Project-Automatic-Seismic-Interpretation-Techniques

This repository contains the presentation(Presentation.pdf),  final report (Report.pdf) and the software for the ACSE-9 module.
This package was developped as part of an internship at Ikon Science (adress: 1st Floor, 1 The Crescent, Surbiton KT6 4BN).
It was supervised by Prof Olivier Dubrule and Lukas Mosser from the Imperial College London and Dr Ehsan Naeini from the Ikon Science.

# Software

This repository contains two main Jupyter notebooks (FCN_Notebook.ipynb and SWC_Notebook.ipynb). FCN_Notebook.ipynb is dedicated to fully convolutional networks, and the SWC_Notebook is dedicated to CNNs (as part of sliding window approach) to do semantic segmentation on seismic datasets. In terms of performance, when we trained our models with only 8 inline slices (out of 401 slices in the entire seismic volume), up to 98.9% pixelwise validation/test accuracies were obtained using the SWC approach, and up to 98.7% validation/test accuracies were obtained using the FCN approach. In terms of speed, FCN approach is the significantly faster approach (by orders of 10^3).


**SWC_Notebook.ipynb:** This notebook is based on the MelanoV (Machine Learning of Voxels) software [Link: https://github.com/LukasMosser/asi-pytorch]. We have edited the original implimentation and our version of this software is provided in the Forties folder in the google drive link. This software mainly contains two python files Train_Model.py (used to train the CNN model) and predict.py (used to make predictions on other inline slices). These predictions are saved into two different files (in a user set directory) of labels.npy and indices.npy which contains the labels and their indices on the seismic cube respectively. The Train_Model.py and predict.py also have dependencies on four different python files of datasets.py, model.py, options.py and utils.py which all have several classes and functions in them, but their main usages are to slice the 65x65x65 seismic cubes (patches) around the indices for training and predicting, define the model to be used for training, set the command- line options, and to save the checkpoints (per epoch) of the trained model respectively.

 The SWC_Notebook.ipynb notebook makes use of this MelanoV software contained within the Forties folder to do  everything from trainig to prediction to visulisation. All the relevant documentation on the usage of this software is provided within the notebook.
 
 **Note:** SWC_Notebook.ipynb makes use of python files 'Train_Model.py', 'predict.py' 'datasets.py', 'model.py', 'options.py' and 'utils.py' in the Forties file (in the shared drive link). This 6 python files inside the Forties file are also copied into the SWC_Notebook.ipynb (in the Utils section), so that the code can be inspected as a whole without going through each file one by one.
 
 **FCN_Notebook.ipynb:** This is a self contained notebook that doesn't have any external dependencies (apart from a CRF library which we install from the google drive link provided below, and the standard python libraries such as numpy, pandas, matplotlib etc.). This notebook does everything from training to prediction to visulisation using FCN models (four different models are provided, two of them are Auto-Encoders and two of them are U-Net models). One of the U-Net models (model 4) is symmetric (i.e. padding and filter sizes adjusted such that the kernel size on the left of U-Net matches that of right side) and size invariant (i.e. output segmentation map will always be same shape as input shape for any given input shape). This makes model 4 applicable to any given dataset without changing anything (only the number of classes parameter on top of model 4 needs to be adjusted).  All the relevant documentation is contained within the notebook.

Apart from the main two notebooks we also have two notebooks (model_avarage.ipynb, and 3D_Visualize.ipynb).
 
**model_avarage.ipynb** : This is to upload the predicted cube segmentation maps from various different models/approaches and model avarage those by taking the mode.

**3D_Visualize.ipynb** : This is contained within the Visualize-3D-Cubes file in the Google drive link. Visualize-3D-Cubes file also contains sample predicted segmetation cubes, seismic amplitudes cubes and the ground truth labellings data. This enables us to visualize 3d arrays in an interactive way with sliding inlines/crosslines and vertical-lines as shown in the appendix of the report. Requirements: pip install segyio and mayavi.

# SETUP INSTRUCTIONS
1. Download this repository or clone it. Then, upload the three jupyter notebooks into Google-Colab.

2. Open a google drive account (its best to not use your personal drive). Four files are shared via the below google drive link. Select the files 'FCN Approach', 'Forties', 'Pydensecrf'. Then, right click and click on add to my own drive. Download the other file 'Visualize-3D-Cubes'.  

3. Once the three files (which contain the datasets and libraries used within the FCN_Notebook.ipynb and SWC_Notebook.ipynb) are in the drive, connect this drive to FCN_Notebook.ipynb and SWC_Notebook.ipynb. Then, you should be able to load the datasets and go through the notebooks to train the models, apply the models etc.

Environment: 3D_Visualize.ipynb in 'Visualize-3D-Cubes', runs on Jupyter (Python 3) whereas, all the other notebooks run on google-colab (Python 3 and GPU enabled).


***
* 'FCN Approach' file contains some pre-trained models for the U-Net model (model 3) which you can load into FCN_Notebook (but this isn't necessary as training time is only a few minutes). It also contains some predictions from pre-trained models (these are used in model averaging in model_average.ipynb).
* 'Forties' file contains our version of the MelanoV software and our dataset. the SWC_Notebook is build as a user guide to the MelanoV software and makes excessive use of 'Forties' file for both reading files and writing files in it.
* 'Pydensecrf' file shared is the Krähenbühl's library for fully connected CRF models with gaussian edge potentials. We copied this repository from https://github.com/lucasb-eyer/pydensecrf
***

If you find this repository useful feel free to cite the repository, the original author's works or drop me a message.

Please respect the licenses of the datasets, the original authors work and of this repository. Thank you
