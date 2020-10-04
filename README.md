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


# Training object detection based on our dataset:
1. Go config folder in darknet and copy yolov3.cfg and rename the copied file to yolov3-custom.cfg
2. Edit yolov3-custom.cfg
Editing part:
- Make comment lines in Testing(#batch=1,#subdivisions=1)
- Uncomment lines in training(batch=64,subdivisions=32) Here subdivisions 16>32>64>128. Chooese depending on your pc's hardware
- max_batches = 4000 (classes*2000)
- steps=3200,3600 (80%,90% of our max_batches)
- Press ctrl+f and find yolo.You'll find 3 yolo layers.Change the classes=2 in 3 yolo layer and filters=21 ((classes+5)*3) in [convolutional] layer above each yolo layers
-save

3. GO to the data folders and make a file named obj.names and edit and save them accordingly(We've changes Airchraft and weapon class to Car and food classes.You have to change accorging you classes)          <br>Car<br>Food<br>

4. Then make a file named obj.name and edit and save them accordingly     <br>classes = 2<br>train = C:/darknet-master/data/train.txt<br>validation = C:/darknet-master/data/test.txt<br>names = C:/darknet-master/data/obj.names<br>backup = C:/darknet-master/backup/<br>

5. Make a backup file in the darknet directory

6. Donwload generate_train.py and put it on darknet directory

7. Open cmd from darknet directory and run command: python generate_train.py   (It will create a file path of every singe dataset images in data folder names as train.txt)

8. Then go to [YOLO: Real-Time Object Detection](https://pjreddie.com/darknet/yolo/) and download the file [pre-trained weight file](https://pjreddie.com/media/files/yolov3.weights)

9. It will download a file named: darknet53.conv.74 , you have to pase it to:  C:\darknet-master\build\darknet\x64

10. Finally run cmd in location: C:\darknet-master\build\darknet\x64 and run a command: <br>darknet.exe detector train C:/darknet-master/data/obj.data C:/darknet-master/cfg/yolov3-custom.cfg darknet53.conv.74

It'll start training and best weight will be saved in C:/darknet-master/backup/yolov3-custom_last.weights

If somehow training stops in the mid, then if you run the training again.It won't strart from begining as we've weights in our backup file

**Few commands:**

- If you want to train from the beginning, then use flag in the end of training command: -clear

To test our model on image:
- darknet.exe detector test C:/darknet-master/data/obj.data C:/darknet-master/cfg/yolov3-custom.cfg C:/darknet-master/backup/yolov3-custom_last.weights 1.jpg

To test our model in video:
-darknet.exe detector demo C:/darknet-master/data/obj.data C:/darknet-master/cfg/yolov3-custom.cfg C:/darknet-master/backup/yolov3-custom_last.weights 1.mp4
