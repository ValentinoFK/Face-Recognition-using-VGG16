# Veritas: Secure, Touchless Attendance System

**Veritas** is an automated attendance tracking application powered by AI. It utilizes Deep Learning (VGG16) for facial recognition and Streamlit for an interactive dashboard, allowing for secure, touchless, and real-time attendance logging.

## 📋 Table of Contents
- [Features](#-features)
- [Tech Stack](#%EF%B8%8F-tech-stack)
- [Project Structure](#-project-structure)
- [Model Details](#-model-details)

## ✨ Features

* **User Authentication:** Secure Login and Registration system using Supabase Auth.
* **Real-Time Face Recognition:** Live webcam feed processing using OpenCV and a fine-tuned VGG16 model.
* **Smart Attendance Logic:** Implements a detection duration threshold (1.5 seconds) to prevent false positives and rapid-fire duplicate logs.
* **Live Dashboard:** Displays system status, recognized class/person, frames per second (FPS), and a real-time clock.
* **Cloud Logging:** Automatically syncs attendance records (Name + Timestamp) to a Supabase database.
* **Local History:** Shows the latest 20 attendance records directly in the UI.

## 🛠️ Tech Stack

* **Frontend & UI:** [Streamlit](https://streamlit.io/)
* **Computer Vision:** [OpenCV](https://opencv.org/) (Haar Cascades for detection)
* **Deep Learning:** [TensorFlow/Keras](https://www.tensorflow.org/) (VGG16 architecture)
* **Backend & Database:** [Supabase](https://supabase.com/) (PostgreSQL + Auth)
* **Language:** Python 3.10+

## 📂 Project Structure

```text
Veritas/
├── .streamlit/
│   └── secrets.toml         # API Keys for Supabase (Not committed)
├── pages/
│   └── Home.py              # Main dashboard: Webcam feed and logs
├── utils/
│   ├── auth.py              # Login/Signup/Logout logic
│   └── model.py             # Face detection and prediction inference
├── __pycache__/             # Compiled Python files
├── app.py                   # Entry point (Login/Register Gateway)
├── labels.json              # Class mapping (Index to Name)
├── supabase_client.py       # Supabase connection initializer
├── vgg_FT_best.keras        # Fine-Tuned Keras Model (Git LFS)
├── VggFaceRecognition.ipynb # Jupyter Notebook used for training
└── requirements.txt         # Project dependencies
```

## 🧠 Model Details

The face recognition core is built upon a **Transfer Learning** approach using the VGG16 architecture.

* **Base Model:** VGG16 (Pre-trained on ImageNet).
* **Architecture:** The top layers of VGG16 were removed and replaced with custom layers for classification.
* **Training:** The model (`vgg_FT_best.keras`) was fine-tuned on a custom dataset containing specific classes.
* **Input Size:** Images are resized to 224x224 pixels before inference.
* **Face Detection:** Before classification, faces are detected and cropped from the video frame using OpenCV's **Haar Cascade Classifiers** (`haarcascade_frontalface_default.xml`).