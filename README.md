# COCO Dataset Preparation, EDA, and YOLOv8 Training

## Overview

This project presents a complete workflow for preparing a COCO-style object detection dataset for model training. It covers dataset downloading, cleaning, verification, exploratory data analysis, annotation conversion, and YOLOv8 training.

The dataset is sourced from Kaggle and processed to ensure that all images and annotations are consistent, valid, and ready for object detection tasks.

## Table of Contents

1. [Project Workflow](#project-workflow)
2. [Setup](#setup)
3. [Dataset Download](#dataset-download)
4. [Data Cleaning](#data-cleaning)
5. [Dataset Verification](#dataset-verification)
6. [Annotation Update](#annotation-update)
7. [Exploratory Data Analysis](#exploratory-data-analysis)
8. [YOLOv8 Training](#yolov8-training)
9. [Additional Notes](#additional-notes)
10. [How to Run](#how-to-run)

---

## Project Workflow

The notebook follows this workflow:

- Download a COCO-style dataset from Kaggle
- Extract and organize the dataset files
- Remove images without annotations
- Update the COCO annotation file after cleaning
- Verify dataset consistency
- Perform exploratory data analysis
- Convert COCO annotations into YOLO format
- Train a YOLOv8 object detection model

---

## Setup

The setup section prepares the working environment.

Main steps include:

- Mounting Google Drive, if running on Google Colab
- Installing required dependencies
- Uploading the Kaggle API token, `kaggle.json`
- Preparing the dataset directory structure

Required packages include:

```bash
pip install kagglehub ultralytics pandas matplotlib seaborn pillow
````

---

## Dataset Download

The dataset is downloaded from Kaggle using the `kagglehub` API.

Dataset source:

```text
evilspirit05/cocococo-dataset
```

After downloading, the dataset is extracted and moved into a dedicated directory:

```text
/content/coco_dataset
```

This makes the dataset easier to manage throughout the cleaning, analysis, and training stages.

---

## Data Cleaning

The cleaning stage ensures that the dataset is consistent and ready for training.

The notebook performs the following tasks:

### Identify Non-Image Files

The dataset directory is scanned to separate image files from other files, such as JSON annotation files.

### Remove Unannotated Images

Images without bounding box annotations are detected by comparing the image files with the COCO annotation file.

Unannotated images are removed to avoid issues during training.

### Clean Annotation Data

The COCO annotation file is updated by removing:

* Deleted image entries
* Annotations related to removed images
* Any inconsistent references between images and annotations

This keeps the dataset synchronized and prevents training errors.

---

## Dataset Verification

After cleaning, several checks are performed to confirm dataset integrity.

The notebook verifies:

* Total number of image files
* Valid image formats, such as `.jpg` and `.png`
* Whether all remaining images have annotations
* Whether the annotation file correctly matches the cleaned dataset

These checks help ensure that the dataset is reliable before training.

---

## Annotation Update

The cleaned COCO annotation file is saved as:

```text
_annotations.coco.json
```

This updated file reflects the final cleaned version of the dataset and is used for further analysis and annotation conversion.

---

## Exploratory Data Analysis

The EDA section provides visual and statistical insights into the dataset.

It includes:

### Categories and Classes

All object categories in the dataset are listed to understand the detection targets.

### Class Distribution

Bar charts are used to visualize the number of object instances per class.

This helps identify class imbalance, which may affect model performance.

### Image Dimensions

The notebook analyzes image widths, heights, and common resolutions.

This is useful for deciding whether resizing or normalization is needed before training.

### Image Quality Check

Low-resolution images, such as images below `300x300` pixels, are detected and reviewed.

Poor-quality images can negatively affect model learning.

### Sample Image Visualization

Random sample images are displayed with their bounding boxes.

This helps visually confirm that annotations are correctly aligned with objects.

### Bounding Box Statistics

The notebook analyzes:

* Bounding box width
* Bounding box height
* Bounding box area
* Bounding box aspect ratio

These statistics help detect unusual annotations or dataset bias.

### Spatial Distribution Analysis

Heatmaps and scatter plots are used to show where objects commonly appear within images.

This can reveal positional bias in the dataset.

---

## YOLOv8 Training

After cleaning and analyzing the dataset, the annotations are converted from COCO format to YOLO format.

### Dataset Conversion

COCO bounding boxes are converted into YOLO format using normalized coordinates:

```text
class_id x_center y_center width height
```

Each image receives a corresponding `.txt` annotation file.

### Environment Setup

YOLOv8 is installed using the official Ultralytics package:

```bash
pip install ultralytics
```

### Model Configuration

A pre-trained YOLOv8 model is used for transfer learning, such as:

```text
yolov8n.pt
```

or

```text
yolov8s.pt
```

### Training Command

Example YOLOv8 training command:

```bash
yolo task=detect mode=train model=yolov8s.pt data=dataset.yaml epochs=50 imgsz=640
```

Main training parameters:

* `task=detect`: object detection task
* `mode=train`: training mode
* `model=yolov8s.pt`: pre-trained YOLOv8 model
* `data=dataset.yaml`: dataset configuration file
* `epochs=50`: number of training epochs
* `imgsz=640`: input image size

---

## Additional Notes

The notebook uses several Python libraries, including:

* `os`
* `json`
* `shutil`
* `collections`
* `PIL`
* `pandas`
* `matplotlib`
* `seaborn`
* `ultralytics`

The workflow is designed to make the dataset clean, organized, and suitable for object detection model training.

The EDA visualizations also help understand class balance, annotation quality, image dimensions, and object placement patterns before training.

---

## How to Run

## Run in Google Colab or Jupyter Notebook

1. Open the notebook in Google Colab or Jupyter Notebook.

2. Upload your Kaggle API token:

   ```text
   kaggle.json
   ```

3. Run the cells sequentially from top to bottom.

4. The notebook will:

   * Download the dataset
   * Extract and organize files
   * Remove unannotated images
   * Update the COCO annotation file
   * Perform EDA
   * Convert annotations for YOLO
   * Train a YOLOv8 model

5. Review the generated plots, statistics, and training outputs.

---

## Run Locally

1. Clone the repository:

   ```bash
   git clone https://github.com/SalmaSaleh7/Autonomous-vehicles-prediction
   cd Autonomous-vehicles-prediction
   ```
   
note: Change the current working directory to the project folder (not the parent folder you cloned into)

2. Create a virtual environment:

   ### Windows

   ```bash
   python -m venv myenv
   myenv\Scripts\activate
   ```

   ### macOS/Linux

   ```bash
   python3 -m venv myenv
   source myenv/bin/activate
   ```

3. Install the required packages:

   ```bash
   pip install -r requirements.txt
   ```

4. Run the application:

   ```bash
   python app.py
   ```

5. Open the application in your browser:

   ```text
   http://localhost:5000
   ```

6. Deactivate the virtual environment when finished:

   ```bash
   deactivate
   ```

---

## Final Output

By the end of this workflow, you will have:

* A cleaned COCO-style dataset
* A synchronized annotation file
* EDA plots and dataset insights
* YOLO-format labels
* A trained YOLOv8 object detection model
* A local application ready to run and test

```
