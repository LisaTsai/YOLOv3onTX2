# YOLOv3onTX2
Try YOLOv3 on TX2 with JetPack3.2

1. Flash TX2 with Jetpack3.2 (Download from https://developer.nvidia.com/embedded/jetpack-notes, need membership)
2. YOLOv3 need cuda 9.0, same as JetPack3.2 provided
3. follow the instructions similar to https://jkjung-avt.github.io/yolov2/
 
$ git clone https://github.com/pjreddie/darknet yolov3
$ cd yolov3
$ nano Makefile

GPU=1

CUDNN=1

OPENCV=1

ARCH= -gencode arch=compute_53,code=[sm_53,compute_53] \
      -gencode arch=compute_62,code=[sm_62,compute_62]

$ make
$ wget https://pjreddie.com/media/files/yolov3.weights
$ ./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights -c 1 

(1 means webcam in /dev/video1, default camera (0) on TX2 cannot be used due to the opencv GStreamer support problem, can rebuild to make it available : https://devtalk.nvidia.com/default/topic/1020837/yolo-with-onboard-camera-pixel-format-error/?offset=12)

Video stream works fine with 1080p, has FPS = 2.9 ~ 3.2

4. try tiny yolo -- not found 

