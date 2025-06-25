# **Player Re-Identification & Tracking using YOLOv11 + BoT-SORT**

This project tracks players in a 15-second video using a fine-tuned YOLOv11 model. It assigns consistent player IDs, even if players go out of frame and re-enter, simulating real-time re-identification.

---

## **Dependencies**

Make sure to install the following in your Colab notebook:

```bash
!pip install ultralytics opencv-python
```

---

## **Files Required**

You need to upload these files to Colab when prompted:

✅ `best.pt` — Your fine-tuned YOLOv11 model for player and ball detection.
✅ `15sec_input_720p.mp4` — The 15-second video for tracking.

---

## **How to Run**

### 1. Upload Required Files

```python
from google.colab import files

print("Upload 'best.pt' (your YOLOv11 model)")
files.upload()

print("Upload '15sec_input_720p.mp4' (your video)")
files.upload()
```

### 2. Run the Tracker

```python
from ultralytics import YOLO

model = YOLO('/content/best.pt')

results = model.track(
    source='/content/15sec_input_720p.mp4',
    save=True,
    show=True,
    tracker='botsort.yaml',
    project='runs/detect',
    name='track',
    exist_ok=True
)
```

* **`save=True`**: Saves the output video with tracking.
* **`show=True`**: Displays the video during processing (only in Colab environments with GUI support).
* **`tracker='botsort.yaml'`**: Uses BoT-SORT tracker for player ID assignment and re-identification.
* **Output Location:** The tracked video will be saved inside `runs/detect/track`.

---

## **Download the Output**

After tracking completes:

```python
import shutil
from google.colab import files

shutil.make_archive('tracked_output', 'zip', 'runs/detect/track')
files.download('tracked_output.zip')
```

This downloads a zipped folder containing the output tracked video.

---

## **Notes**

* This setup assumes `botsort.yaml` is pre-configured in the Ultralytics environment.
* The model provided (`best.pt`) is fine-tuned for detecting players and the ball.
* This pipeline is designed for quick testing and demo purposes on Colab.
