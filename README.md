# SeleniumSight : an Object Detection Agent for UI Testing Automation #

Welcome to the replication material for our research study. The purpose of this document is to provide all necessary details, datasets, and codes to reproduce the results presented in our manuscript. We believe in the importance of transparency and reproducibility in research. Given the double-blind review process, identifiable information has been removed to maintain the anonymity of the authors. We encourage reviewers to make use of these materials and provide feedback or raise any queries they might have.

## Table of Contents ## 
<ul>
  <li>Dataset Description</li>
  <li>Training Object Detection Models</li>
  <li>Training results and figures</li>
  <li> Running inference on yolov8 for identifying web elements
  
</ul>


### Dataset Description ###

### Objective ###
Autonomously generate a dataset of 6,000 annotated screenshots from Wikipedia pages. These annotations are tailored to train object detection models, specifically YOLOv3, YOLOv5, and YOLOv8, enabling them to recognize and locate web elements on screenshots.

### Key Components ###

#### Libraries and Dependencies
- **Scrapy**: A web crawling framework that provides the foundation for efficient Wikipedia exploration.
- **Selenium**: Utilized for its headless Chrome browser, ensuring accurate rendering and interaction with Wikipedia pages.
- **OpenCV (cv2)**: Essential for image processing, especially for drawing bounding boxes on detected web elements.
- **Multiprocessing**: Aims to enhance data generation speed through concurrent processing.

### Dataset Generation Pipeline

#### Initialization
- A headless Chrome browser instance is launched.
- The browser's dimensions are standardized to a typical desktop viewport.
- Wikipedia URLs are the entry points, steering the direction of the crawl.


### Training Object Detection Models###

To train the YOLO models, we used the ultralytics pip package.
Please refer to the official documentation on how to install [Official Documentation](https://docs.ultralytics.com/#where-to-start)
To start training, unzip the wiki.zip file in the current directory and make sure you have the data.yml file.
After installing ultralytics, you may start training via the command line instantly by running:
```bash
yolo task=detect \
mode=train \
model=yolov8x.pt.pt \
data={dataset.location}/data.yaml \
epochs=150 \
imgsz=640
```
In this example we are using the yolov8x model, the largest one. Feel free to select any other model from the official documentation.

### Training results and figures ###

The folder training_results contains the results of the best performing model YOLOv8.
When the training is finished, you will get a folder with the same structure.

### Inference ###

If you want to use the trained model we got, you may use the last.pt (Pytorch) model file and you may run inference on a wikipedia screenshot of your choice by running:
```bash
yolo task=detect \
mode=predict \
model=last.pt \
conf=0.5 \
source={images_folder}
```
Please remember to properly adjust paths.

