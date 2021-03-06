# 2021-VRDL-HW2

## Environment

* Ubuntu 18.04.5 LTS (GNU/Linux 4.15.0-39-generic x86_64)

## Requirements

docker (recommanded):

```setup
# create the docker container, you can change the share memory size if you have more.
nvidia-docker run --name yolov4 -it -v your_coco_path/:/coco/ -v your_code_path/:/yolo --shm-size=64g nvcr.io/nvidia/pytorch:20.11-py3

# apt install required packages
apt update
apt install -y zip htop screen libgl1-mesa-glx

# pip install required packages
pip install seaborn thop

# install mish-cuda if you want to use mish activation
# https://github.com/thomasbrandon/mish-cuda
# https://github.com/JunnYu/mish-cuda
cd /
git clone https://github.com/JunnYu/mish-cuda
cd mish-cuda
python setup.py build install

# go to code folder
cd /yolo
```

To install requirements:

```setup
pip install -r requirements.txt
```

※ For running Mish models, please install https://github.com/thomasbrandon/mish-cuda

## Training

```setup
python train.py --device 0 --batch-size 8 --img 640 640 --data hw2.yaml --cfg cfg/hw2.cfg --weights 'hw2.weights' --name hw2 --epoch 60 
```

## Weight for Training Model

You can download the file here:

- [The file of weight](https://drive.google.com/file/d/1gjz7FFvbhG_0QbPQnWWrZmDXy_NqmVdD/view?usp=sharing)

## Testing

```setup
python test.py --img 640 --conf 0.0001 --batch 32 --device 0 --data hw2.yaml --cfg cfg/hw2.cfg --weights weights/best.pt --iou-thres 0.4  --task test --names data/hw2.names --save-json
```

## Testing Result

![test_batch2_pred](https://user-images.githubusercontent.com/68366624/143426317-41dc4d06-5850-41ab-9e42-ba537c9cab5a.jpg)

![test_batch3_pred](https://user-images.githubusercontent.com/68366624/143426391-7df58b8b-2a81-4890-b7e7-e7ad9bef6680.jpg)

## Speed benchmark

The following figure is the screenshot of my benchmark result, where inference time per image is 0.081907 seconds.
![image](https://user-images.githubusercontent.com/68366624/143500164-67b0687d-4f96-4b3c-a703-49c7b9d853ec.png)



## Google Drive link

This contains all the files that need to be used.
- [Google Drive](https://drive.google.com/drive/folders/1qCjpj7PW43pt3TibQhNta8HEryYeurDM?usp=sharing)
