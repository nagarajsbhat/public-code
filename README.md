# Scene Understanding Challenge for Autonomous Navigation in Unstructured Environments

Code for working with the dataset used for the [Scene Understanding Challenge for Autonomous Navigation in Unstructured Environments](http://cvit.iiit.ac.in/scene-understanding-challenge-2018/). For details of getting the dataset and updates see:

- http://cvit.iiit.ac.in/scene-understanding-challenge-2018/ 
- http://cvit.iiit.ac.in/autonue2018/

**For using first add helpers/ to $PYTHONPATH**

## Dataset Structure

The structure is similar to the cityscapes dataset. That is:
- gtFine/<split>/<drive_no>/<6 digit img_id>_gtFine_polygons.json for ground truths
- leftImg8bit/<split>/<drive_no>/<6 digit img_id>_leftImg8bit.png for image frames

Furthermore for training, label masks needs to be generated as described bellow resulting in the following files:
- gtFine/<split>/<drive_no>/<6 digit img_id>_gtFine_labellevel3Ids.png
- gtFine/<split>/<drive_no>/<6 digit img_id>_gtFine_instancelevel3Ids.png

## Labels

See helpers/anue_labels.py

## Generate Label Masks (for training/evaluation)

python preperation/createLabels.py --datadir $ANUE --id-type $IDTYPE --color [True|False] --instance [True|False] --num-workers $C

- ANUE is the path to the AutoNUE dataset
- IDTYPE can be id, csId, csTrainId, level3Id, level2Id, level1Id. For standart AutoNUE training level3Id should be used.
- color True  generates the color masks
- instance True generates the instance masks with the id given by IDTYPE
- C is the number of threads to run in parallel

## Viewer

First generate label masks as described above. To view the ground truths / prediction masks at different levels of heirarchy use:

python viewer/viewer.py ---datadir $ANUE

- ANUE has the folder path to the dataset or prediction masks with similar file/folder structure as dataset.

TODO: Make the color map more sensible.


## Evaluating IoUs

First generate labels masks. Then

python evaluate/evaluate_mIoU.py --gts $GT  --preds $PRED  --num-workers $C

- GT is the folder path of ground truths containing <drive_no>/<img_no>_gtFine_labellevel3Ids.png 
- PRED is the folder paths of predictions with the same folder structure and file names.
- C is the number of threads to run in parallel

## Work in Progress

- instance metrics
- mIoUs at level2 and level1
- viewer tool for masks

## Acknowledgement

Some of the code was adapted from the cityscapes code at: https://github.com/mcordts/cityscapesScripts/ 

