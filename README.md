# Face Recognition Academy

A desktop face-recognition application for registering people, collecting face images through a webcam, generating facial embeddings, training a classifier, and recognizing faces in real time.

> **Legacy project:** This project uses Python 3.6-era libraries, TensorFlow 1.14, Keras 2.1, MXNet, MTCNN, and InsightFace. A modern Python or TensorFlow environment may require code and dependency updates.

## Features

- Collect face images from a webcam
- Generate 112 × 112 face embeddings with InsightFace
- Train a Keras/softmax face classifier
- Register and identify users through a Tkinter desktop interface
- Real-time face detection and recognition from a camera
- Store embeddings and model artifacts locally

## Project Structure

```text
.
├── datasets/
│   └── train/                 # Training images grouped by person name
├── src/
│   ├── app.py                 # Tkinter application entry point
│   ├── clientApp.py           # Registration, embedding, training, prediction helpers
│   ├── collect_training_data/ # Webcam image collection
│   ├── detect_faces_mtcnn/    # MTCNN detection configuration and utilities
│   ├── face_embedding/        # InsightFace embedding extraction
│   ├── predictor/             # Live recognition pipeline
│   ├── training/              # Keras/softmax model training
│   ├── faceEmbeddingModels/   # Generated embeddings, labels, and trained model
│   └── insightface/           # Bundled InsightFace deployment/model files
├── requirements.txt
└── How to run.txt
```

## Requirements

- Python 3.6.9 (recommended for compatibility with the pinned dependencies)
- Conda or a virtual environment
- Webcam
- A desktop environment capable of displaying Tkinter/OpenCV windows
- CPU/GPU drivers and software compatible with TensorFlow 1.14 and MXNet 1.5

> On Apple Silicon Macs, this dependency stack is unlikely to install or run without substantial compatibility updates.

## Installation

From the project root:

```bash
conda create -n facerecognition python=3.6.9
conda activate facerecognition
python -m pip install --upgrade pip setuptools wheel
python -m pip install -r requirements.txt
```

Package installation may need platform-specific changes, especially for `dlib`, `mxnet`, `opencv-python`, and `tensorflow`.

## Running the Application

The application is designed to be run from the `src` directory because several internal paths are relative to that location:

```bash
cd src
python app.py
```

If importing the project from the repository root, run:

```bash
PYTHONPATH=. python src/app.py
```

The first command is the conventional launch method for this legacy layout.

## Usage

1. **Register a person**
   - Enter a client ID, employee ID, name, and other displayed details.
   - Click **Take Images**.
   - Look at the webcam until 50 face images are collected.
   - Images are stored below `datasets/train/` in a folder named after the person.

2. **Train the model**
   - Click **Train Images**.
   - The app extracts embeddings, saves `embeddings.pickle`, and trains `my_model.h5`.

3. **Recognize a face**
   - Click **Predict**.
   - The camera window should show a detected face and the predicted identity.
   - Press `q` in the OpenCV window to stop capture when supported.

## Generated Model Files

Generated training artifacts are saved in `src/faceEmbeddingModels/`:

- `embeddings.pickle` — extracted face embeddings and names
- `le.pickle` — label encoder
- `my_model.h5` — trained Keras classifier

Do not commit generated personal face images or trained artifacts if they contain private biometric data.

## Troubleshooting

- **Camera does not open:** Confirm that OpenCV can access the webcam and that camera permissions are enabled.
- **Model or insightface files are missing:** Verify the files inside `src/insightface/models/model-y1-test2/` exist.
- **Tkinter is missing:** Install the Tk/Tcl package provided by your operating system or Conda distribution.
- **TensorFlow or MXNet installation fails:** Use Python 3.6.9 and a compatible CPU/GPU environment; the pinned versions predate Apple Silicon and many current operating systems.
- **Images are saved in the wrong location:** Launch the application from `src`, since several configured paths are relative to the working directory.
- **A module cannot be imported:** Set the repository root on `PYTHONPATH` and avoid mixing old iNeuron-style paths with renamed package names.

## Security and Privacy

This application processes and stores biometric face data. Obtain consent before capturing people, restrict access to datasets and model files, and follow applicable biometric-data, privacy, and retention regulations.
