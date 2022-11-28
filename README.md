# Seq_nms_YOLO
This project is adapted from https://github.com/melodiepupu/seq_nms_yolo to simplify the execution of Seq-NMS and YOLOv2 approaches for video object detection.
#### Membres: Yunyun SUN, Yutong YAN, Sixiang XU, Heng ZHANG
#### Adapted by: Alfredo Sanz, Marcelina Loyola

---

## Introduction

![](img/index.jpg) 

This project combines **YOLOv2**([reference](https://arxiv.org/abs/1506.02640)) and **seq-nms**([reference](https://arxiv.org/abs/1602.08465)) to realise **real time video detection**.


All the steps have to executed in a terminal linux with Anaconda

## Steps
1. Open a terminal.
2. Clone the repository: 
   - `git clone https://github.com/Alfredo-Marcelina/Seq_nms_YOLO.git`
3. Enable permissions 
   - `chmod -R 755 Seq_nms_YOLO`
4. Open the folder seq_nms_YOLO:
   - `cd Seq_nms_YOLO`
5. There are two way to create the environment MANUALLY or DIRECTLY:
- Manually:
   - `conda create --name Yolo_e python=2.7`
   - `source activate Yolo_e` (It is important have python 2.7 because this repository is implemented in this version)
  - Install Tensorflow Object Detection API 
   - cv2: `conda install opencv`
   - matplotlib: `conda install matplotlib`
   - scipy: `conda install -c anaconda scipy`
   - tensorflow: `pip install tensorflow-gpu`
   - pillow: `conda install -c anaconda pillow`
   - tf_object_detection: `pip install tf_object_detection`
 - Directly
   - `source activate`
   - `conda env create -f Yolo_envi.yml`
   - `conda activate Yolo_envi`
 6. Create a project
   - Make the project: `make`
   - Set up the development environment by modifying the PATH and LD_LIBRARY_PATH variables:
      - `export PATH=/usr/local/cuda-10.1/bin${PATH:+:${PATH}}`
      - `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-10.1/lib64`
      - `export LIBRARY_PATH=$LIBRARY_PATH:/usr/local/cuda-10.1/lib64`
   - Download weights and tiny weights:
      - `wget https://pjreddie.com/media/files/yolo.weights`
      - `wget https://pjreddie.com/media/files/yolo-tiny.weights`
  7. Go to file to the video directory (/seq_nms_YOLO/video)
      - `cd video`
  8. Copy a video file to the video directory (/seq_nms_YOLO/video), for example, input.mp4 or input.avi, however you can use the videos that are insade of the folder:
  
     - v_ApplyLipstick_g21_c01.avi
     - v_Archery_g07_c01.avi
     - v_BabyCrawling_g11_c01.avi
     - v_BalanceBeam_g18_c01.avi
     - v_HorseRace_g01_c01.avi
     
   9. From the directory (/seq_nms_YOLO/video):
      - `python video2img.py -i input.avi`
      - `python get_pkllist.py`
      
   10. Return to root directory seq_nms_YOLO `cd ..` to generate output images in video/output: 
    
      - If you want to run only Yolo v2 `python yolo_seqnms.py --Seq_Nms 0 --Nms 0`
      - If you want to run Seq-NMSYOLOv2 `python yolo_seqnms.py --Seq_Nms 1 --Nms 1`
      - If you want to run Seq-NMSYOLOv2 but without the Seq_NMS post processing `python yolo_seqnms.py --Seq_Nms 0 --Nms 1`
      - If you want to run Seq-NMSYOLOv2 but desactivating NMS with the intention to not detect the relevant detections then  `python yolo_seqnms.py --Seq_Nms 1 --Nms 0`

IMPORTANT: This step will fail if the Tensorflow Object Detection API is not installed correctly, start again with all the steps.

- If you want to reconstruct a video from these output images, you can go to the video directory (/seq_nms_YOLO/video) and run:
   - `cd video`
   - `python img2video.py output.mp4` or `python img2video.py -i output`
 The results would be available in the video folder `output.mp4`.


     ![ApplyLipstick_seq1_nms1](https://user-images.githubusercontent.com/118300060/204159412-9a9158d5-90fb-41ae-9657-f331b5849af1.gif)
     ![ApplyLipstick_seq0_nms0](https://user-images.githubusercontent.com/118300060/204159416-ddcd4818-4eff-460d-9450-ad239a140c41.gif)


## Reference

This project copies lots of code from [darknet](https://github.com/pjreddie/darknet) , [Seq-NMS](https://github.com/lrghust/Seq-NMS) and  [models](https://github.com/tensorflow/models).

Some instructions were extracted from: https://docs.nvidia.com/cuda/cuda-quick-start-guide/index.html


