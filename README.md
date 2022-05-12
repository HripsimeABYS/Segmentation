# Segmentation

This repository contains scripts for 3D Unet architechture which is based on integrated MONAI into an existing PyTorch medical DL program. 

* Install the requirements.txt file by using 'pip install -r requirements.txt'
* The instalation steps for pytorch and monai is written in "installation.txt" file.

Description of Dataset, extraction of data and CSV file:
* The Pelvis dataset can be downloaded https://zenodo.org/record/4588403#.Ym-WotpBy3B
* Download Images: CTPelvic1K_dataset6_data.tar.gz
* Download Masks: CTPelvic1K_dataset6_Anonymized_mask.tar.gz
* Create a folder "Data" on your D drive where all images and masks will be extracted. 
* In order to extract images write in command prompt and in your "Data" folder you will have a "CTPelvic1K_dataset6_data" folder with 103 images.
tar -xvzf C:\Users\Yourname\Downloads\CTPelvic1K_dataset6_data.tar.gz -C D:\Data
* In order to extract masks write in command prompt and in your "Data" folder you will have a "ipcai2021_dataset6_Anonymized" folder with 103 masks.
tar -xvzf C:\Users\Yourname\Downloads\CTPelvic1K_dataset6_Anonymized_mask.tar.gz -C D:\Data

By using "data_github.csv" file, "CustomDataset" class in the scripts will automaticly select "train_images", "train_masks", "test_images" and "	test_masks".

* Dataset: dataset6 (CLINIC) 
* Target: Pelvis
* Modality: CT
* Format: NIFTI
* Size: 60 cases (41 Training + 19 Testing)

Labels: 
* 0: background, 
* 1: sacrum, 
* 2: right_hip, 
* 3: left_hip, 
* 4: lumbar_vertebra    




Description of python scripts:

1) train.py --> 3D Unet training which works with Early Stopping. In this file you need to modify only "train_dir" and write the path where your training dataset is stored. If you are getting a memory error (CUDA out of memory), in "train_loader" change batch_size to 1.

2) evaluate.py --> In this file you need to modify "train_dir" and "test_dir". You need to write paths where your training and testing datasets are stored. It evaluates the trained model on testing dataset and verify the dice score of each case. 
 
3) predict.py --> In this file you need to modify only "model_dir" and write the path where the model file "best_metric_model.pth" is saved after training. It uploads one image and output gives one segmented mask: 
python predict.py -i image.nii.gz -o seg.nii.gz
     
4) slicer.py -->  In this file you don't need to modify anything, just place the file in the same folder where is a segmented mask to run the script. It transforms segmented mask to make it suitable for 3D slicer visualization: 
python slicer.py -i seg.nii.gz -o name.nii.gz

5) pytorchtools.py --> for early stopping and must be placed in the same folder where the train.py file is located. 
