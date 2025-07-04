````markdown
# OLOv8 Training & Object Tracking No Praking Sign

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
