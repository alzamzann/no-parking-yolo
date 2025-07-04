````markdown
# RambuSCAP12 - YOLOv8 Training & Object Tracking

This repository contains code for training a YOLOv8 model using a custom dataset from Roboflow to detect traffic signs ("Rambu") and perform object tracking on video input.

## 📁 Project Structure

- Trains a YOLOv8 model on the dataset.
- Exports the best trained model.
- Tracks objects from a video using the trained model.

## 🔧 Requirements

This project is intended to be run on **Google Colab**. Make sure to have:

- Python 3.x or Google Collab
- Roboflow account & API key
- Google Drive for storing input/output
- A video file for testing (e.g., `rambu_test2.mp4`)

## 📦 Installation

Install dependencies using the following commands:

```bash
!pip install roboflow
!pip install ultralytics
````

## 🚀 Usage

### 1. Dataset Download from Roboflow

```python
from roboflow import Roboflow
rf = Roboflow(api_key="YOUR_API_KEY")
project = rf.workspace("testi-ymodf").project("rambuscap12")
version = project.version(2)
dataset = version.download("yolov8")
```

> Replace `"YOUR_API_KEY"` with your actual Roboflow API key.

### 2. Mount Google Drive

```python
from google.colab import drive
drive.mount('/content/drive')
```

### 3. Load and Train YOLOv8 Model

```python
from ultralytics import YOLO
model = YOLO('yolov8n.pt')  # load pretrained model
results = model.train(data='/content/RambuSCAP12-2/data.yaml', epochs=65, imgsz=640)
```

> Change the `data` path if necessary to point to your `data.yaml`.

### 4. Zip and Export the Trained Model

```python
import zipfile, os

def zip_dir(folder_path, output_path):
    with zipfile.ZipFile(output_path, 'w', zipfile.ZIP_DEFLATED) as zipf:
        for root, _, files in os.walk(folder_path):
            for file in files:
                zipf.write(os.path.join(root, file), os.path.relpath(os.path.join(root, file), folder_path))

folder_to_zip = '/content/runs/detect/train'
zip_output_path = '/content/runs/noparking.zip'
zip_dir(folder_to_zip, zip_output_path)
```

### 5. Run Object Tracking on a Video

```python
from ultralytics import YOLO

model = YOLO('/content/runs/detect/train/weights/best.pt')
results = model.track(source='/content/drive/MyDrive/TESTING_SCAP12/rambu_test2.mp4', save=True)
```

## 🎯 Results

* The trained model is saved in: `/content/runs/detect/train/weights/best.pt`
* The zipped model is saved as: `noparking.zip`
* Tracked video with bounding boxes is saved in the same directory as the input.

## 📌 Notes

* Make sure the input video (`rambu_test2.mp4`) exists in your Google Drive.
* The dataset (`RambuSCAP12`) is expected to follow YOLOv8 format.

## 📚 References

* [Roboflow Docs](https://docs.roboflow.com/)
* [Ultralytics YOLOv8](https://docs.ultralytics.com/)
