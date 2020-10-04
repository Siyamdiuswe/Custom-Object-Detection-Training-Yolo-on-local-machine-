# Train YOLOv3 Custom Object Detector with Darknet 

You can follow this video too!

Link: [Custom Object Detecto](https://www.youtube.com/watch?v=zJDUhGL26iU&t=270s&ab_channel=TheAIGuy)

**First we have to collect and manage dataset**

Link: [Google Image Datasets API](https://storage.googleapis.com/openimages/web/visualizer/index.html?set=train&type=segmentation&r=false&c=%2Fm%2F05r5c)
---
First, Download 

*We can use simple command to download dataset of different classes*
command: python main.py downloader --classes Aircraft Weapon --type_csv train --limit 1000 --multiclsses 1

*Explaination*
1. --classes Aircraft Weapon:Aircraft and Weapon are classes that we want to download 
2. --type_csv train : We want training dataset
3. --limit 1000 : not to download more than 1000 images(For each class)
4. --multiclsses 1: We want our classes to be in one folder

