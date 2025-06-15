# 🐶 Dogs Count with YOLOv5

A real-time object detection app that counts and highlights dogs in a video feed using YOLOv5. Designed for use on NVIDIA Jetson devices with a live webcam input.

---

### 📸 Features

- Runs on NVIDIA Jetson with GPU acceleration
- Captures real-time video from `/dev/video0`
- Uses YOLOv5 (v6.0) for object detection
- Detects only **dogs** (COCO class ID: `16`)
- Displays bounding boxes and count overlay in real-time

---

### 🐧 Running on Jetson via Docker

To launch the application inside an NVIDIA Jetson-compatible Docker container:

```bash
sudo docker run -it \
  --runtime nvidia \
  --network host \
  --device=/dev/video0 \
  nvcr.io/nvidia/l4t-ml:r32.5.0-py3
```

---

### 🌐 Accessing Jupyter Notebook

Once inside the container, Jupyter Notebook will be available at:

```
http://192.168.55.1:8888/
```

> 🔐 A token might be required the first time — check the terminal output in the Docker container for the correct URL.

---

### 🛠️ Setup Instructions (inside Jupyter)

In the Notebook, run the following commands to install dependencies and download the model:

```bash
# Install required libraries
apt-get update
apt-get install -y python3-pip libopencv-dev
pip3 install --upgrade pip
pip3 install torch torchvision torchaudio
pip3 install numpy opencv-python matplotlib seaborn Pillow requests scipy tqdm

# Clone YOLOv5 and get model
git clone -b v6.0 https://github.com/ultralytics/yolov5.git
cd yolov5
wget https://github.com/ultralytics/yolov5/releases/download/v6.0/yolov5s.pt
```

---

### ▶️ Running the Notebook

Open `dogscount.ipynb` in Jupyter and run all cells. The camera will start and dog detection will begin automatically.

Example output overlay:

```
Dogs Detected: 2
```

---

### 📂 Project Structure

- `dogscount.ipynb`: Main notebook
- `yolov5/`: YOLOv5 source code (cloned from GitHub)
- `yolov5s.pt`: Pre-trained YOLOv5 small model

---

### ⚠️ Notes

- Make sure your webcam is accessible as `/dev/video0`.
- This notebook is best run in a Jupyter environment on Jetson.
- For better accuracy, you can use other YOLOv5 models like `yolov5m`, `yolov5l`, etc.

---

### 📃 License

This project is released under the **MIT License**. The YOLOv5 model is subject to its own license (GPLv3).
