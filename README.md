# Train YOLOv3 Custom Object Detector with Darknet 

You can follow this video too!

Link: [Custom Object Detecto](https://www.youtube.com/watch?v=zJDUhGL26iU&t=270s&ab_channel=TheAIGuy)

**First we have to collect and manage dataset**

Link: [Google Image Datasets API](https://storage.googleapis.com/openimages/web/visualizer/index.html?set=train&type=segmentation&r=false&c=%2Fm%2F05r5c)
---
1. Download or clone Train-YOLOv3-Custom-Object-Detector-with-Darknet repository

[Link](https://github.com/Siyamdiuswe/Train-YOLOv3-Custom-Object-Detector-with-Darknet)

2. Open command prompt from the directory where you've donwloaded/cloned the repository

3. Run on the cmd: python main.py downloader --classes Aircraft Weapon --type_csv train --limit 1000 --multiclsses 1
It will download dataset consist of classes that we want.

*Explaination*
- --classes Aircraft Weapon:Aircraft and Weapon are classes that we want to download 
- --type_csv train : We want training dataset
- --limit 1000 : not to download more than 1000 images(For each class)
- --multiclsses 1: We want our classes to be in one folder

Then data will be downloaded in OID/Dataset/train folder

4. Change the class.txt according to the classes of the dataset.For aour case, it was <br>Aircraft<br>Weapon

5. Run python convert_annotations.py . It will create an extra annotation file after each of the image file

6. Copy all data from Aircraft_Weapon folderr and paste them into C:\darknet-master\data\obj folder

*Our dataset creating step is complete*
---
