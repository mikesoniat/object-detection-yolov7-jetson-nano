# object-detection-yolov7-jetson-nano
Object Detection with Jetson Nano and YOLO v7

This repository includes my PowerPoint presentation, which describes the software libraries used, as well as step by step instructions on how to install YOLOv7 on the Jetson Nano. I've also included my source files (photos and video) and the detected files with yolo results.

<h1>Project Goals</h1>
<ul>
<li> Experiment with YOLO v7.</li>
<li>Use Python, PyTorch, TorchVision, and OpenCV for deep learning and object detection.</li>
<li>Use YOLO v7 to</li>
<ul>
<li>Detect faces and objects on photos.</li>
<li>Detect faces and objects on videos.</li>
<li>Detect faces and objects on live camera stream.</li>
</ul>
</ul>

Implementation Notes:
YOLO v7 on Jetson Nano

* Setup Jetson Nano 
    * https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#intro 
    * Download the latest SD card image from:  
        * https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#write 
    * Boot up Jetson Nano and do initial setup 
    * Download and install pre-requisites 
        * $ sudo apt update 
        * $ sudo apt install python3-pip 
        * $ pip check  
        * $ sudo apt install libfreetype6-dev 
        * $ pip3 install --upgrade pip setuptools wheel 
        * $ python3 -m pip install --upgrade --force-reninstall pip 
        * $ pip3 install numpy==1.19.4 
    * Download and install YOLO v7 repository 
        * $ git clone https://github.com/WongKinYiu/yolov7.git 
        * $ cd yolov7 
        * Edit then run requirements.txt file 
            * $ gedit requirements.txt 
            * comment out matplotlib, numpy, opencv-python, torch, torchvision, and thop by placing a # in front 
                * save file and exit 
            * $ pip3 install -r requirements.txt 
        * Download and install Pytorch 
            * Download PyTorch v1.8.0 from https://forums.developer.nvidia.com/t/pytorch-for-jetson/72048 
                * download torch-1.8.0-cp36-cp36m-linux_aarch64.whl 
                * $ wget https://nvidia.box.com/shared/static/p57jwntv436lfrd78inwl7iml6p13fzh.whl -O torch-1.8.0-cp36-cp36m-linux_aarch64.whl 
                * $ sudo apt-get install python3-pip libopenblas-base libopenmpi-dev libomp-dev 
                * $ pip3 install Cython 
                * $ pip3 install torch-1.8.0-cp36-cp36m-linux_aarch64.whl 
            * Download and install TorchVision 
                * $ sudo apt-get install libjpeg-dev zlib1g-dev libpython3-dev libavcodec-dev libavformat-dev libswscale-dev 
                * $ git clone --branch v0.9.0 https://github.com/pytorch/vision torchvision   # see below for version of torchvision to download 
                * $ cd torchvision 
                * $ export BUILD_VERSION=0.9.0   
                * $ python3 setup.py install --user 
                * $ cd ../  
        * Testing 
            * python3 detect.py --weights yolov7-tiny.pt --conf 0.25 --img-size 640 --source inference/images/horses.jpg 
                * first time run matplotlib builds the font cache and yolov7-tiny.pt is downloaded 
                * start detection: 
                    * on camera: python3 detect.py --weights yolov7-tiny.pt --source 1 
                    * on camera: python3 detect.py --weights yolov7-tiny.pt --conf 0.25 --img-size 640 --source 1 
                    * on camera: python3 detect.py --weights yolov7-tiny.pt --conf 0.25 --img-size 480 --source 1 
                    * on an image file: python3 detect.py --weights yolov7-tiny.pt --conf 0.25 --img-size 640 --source inference/images/horses.jpg 
            * street video 
                * https://www.youtube.com/watch?v=MNn9qKG2UFI 
                * recorded with screenshot for first 55 seconds 
                    * saved file StreetView2.mov 
                * Long Shot of People Walking Along Busy Street In Oxford 
                    * https://www.videvo.net/video/long-shot-of-people-walking-along-busy-street-in-oxford-england/608577/ 
                    * saved file People.mp4 
                * copied to flashdrive and to Jetson Nano in yolo/yolov7/inference/images folder 
                * ran $ python3 detect.py --weights yolov7-tiny.pt --conf 0.25 --img-size 640 --source inference/images/People.mov
                  
* Links 
* https://www.hackster.io/spehj/deploy-yolov7-to-jetson-nano-for-object-detection-6728c3 
* https://blog.roboflow.com/how-to-deploy-yolov7-to-jetson-nano/ 
* https://github.com/Qengineering/YoloV7-ncnn-Jetson-Nano 
* https://github.com/patharanordev/jetson-nano-gstreamer-yolov7 

