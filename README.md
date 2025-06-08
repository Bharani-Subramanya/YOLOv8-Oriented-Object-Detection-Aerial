# YOLOv8-Oriented-Object-Detection-Aerial


📂 Datasets Used:

This project utilizes two major aerial datasets for training and evaluating oriented object detection models using **YOLOv8-OBB**.

1. DOTA v1.5 (Dataset for Object Detection in Aerial Images)

* Description: Aerial images captured from multiple sensors/platforms, annotated with **Oriented Bounding Boxes (OBB)**.
* Use Case: Ideal for training and evaluating models that detect rotated objects in aerial views.
* Classes: 15 object categories (e.g., ship, plane, vehicle, etc.)


Download Links (Google Drive):

* [📦 Training Set]
* [📦 Validation Set]
* [📦 Testing Set]
  
🔗 **Official Page**: [DOTA Website](https://captain-whu.github.io/DOAI2019/dataset.html)


Suggested Folder Structure:
```
datasets/
└── dota/
    ├── train/
    ├── val/
    └── test/
```


2. VisDrone (Vision Meets Drone)

* **Description**: A large-scale dataset captured by drones flying in various urban/suburban environments.
* **Task Used**: **Task 1 – Object Detection in Images**
* **Challenges**: Occlusion, scale variation, and dense objects.

📥 **Download Task 1 Sets**:

* [📦 VisDrone2019-DET-train.zip]
* [📦 VisDrone2019-DET-val.zip]
* [📦 VisDrone2019-DET-test-dev.zip]

🔗 **Official Repo**: [VisDrone-Dataset GitHub](https://github.com/VisDrone/VisDrone-Dataset)

📁 **Suggested Folder Structure**:

```
datasets/
└── visdrone/
    ├── VisDrone2019-DET-train/
    ├── VisDrone2019-DET-val/
    └── VisDrone2019-DET-test-dev/
```
---
📌 **Note**: For training YOLOv8-OBB models, annotations must be converted to **YOLO OBB format**.
If needed, we can provide a converter script for DOTA and VisDrone datasets.

---

---

🔄 Dataset Preparation via Roboflow

For this project, I used **[Roboflow](https://roboflow.com/)** to streamline dataset management and augmentations.

---

### Steps I Followed:

1. **Uploaded the dataset** to Roboflow (e.g., DOTA or VisDrone custom-prepared snippets).
2. Chose **"Object Detection (OBB)"** as the project type.
3. Applied **data augmentations** like:

   * Rotation
   * Flipping
   * Scaling
   * Brightness adjustments (if needed)
4. Exported the dataset in **YOLOv8 format (snippet version)**.

---


You can **automatically download the dataset** while running the notebook in Google Colab using the following snippet:

```python
# Create dataset directory and change into it
!mkdir {HOME}/datasets
%cd {HOME}/datasets

# Install Roboflow
!pip install roboflow

# Download the dataset from Roboflow
from roboflow import Roboflow

# Initialize Roboflow with your API key
rf = Roboflow(api_key="DR4agSFbtjXAg0cXPCmj")

# Access your specific project and version
project = rf.workspace("navuluru-venkata-bharani-subramanya-kumar-wpqql").project("dottttta1.0")
version = project.version(9)

# Download in YOLOv8 format with Oriented Bounding Boxes (OBB)
dataset = version.download("yolov8-obb")
```

### After running:

* Your dataset will appear in the **left-side file browser** in Colab under `/content/datasets`.
* It includes pre-split folders: `train/`, `valid/`, `test/`, and a `data.yaml` config file for training.

---

### 🔗 Roboflow Project Link
> [Roboflow - dottttta1.0 Dataset](https://universe.roboflow.com/navuluru-venkata-bharani-subramanya-kumar-wpqql/dottttta1.0)

---


---

### 📁 Updating `data.yaml` (After Roboflow Download)

After downloading the dataset via Roboflow, you must **verify or update the `data.yaml` file** to ensure the paths to your training, validation, and test sets are correct.

Here's how to do it:

---

## 🛠️ Step: Edit `data.yaml`

Once the dataset is downloaded using the snippet provided, you’ll find a file called `data.yaml` inside the dataset directory (`/content/datasets/<your_dataset_name>`).

### ✅ Check that it looks like this:

```yaml
train: /content/datasets/dottttta1.0-9/train/images
val: /content/datasets/dottttta1.0-9/valid/images
test: /content/datasets/dottttta1.0-9/test/images

nc: 10  # Number of object classes (update if different)
names: ['car', 'bus', 'truck', 'motorcycle', 'bicycle', 'van', 'pedestrian', 'construction_vehicle', 'traffic_sign', 'others']
```

> 🔁 Change the `nc` and `names` list according to your dataset.
> The folder path should match the version name and structure you downloaded via Roboflow.

---

### 📍 Tip:

* If you're training in **Google Colab**, full paths starting with `/content/...` are required.
* If you’re unsure of your dataset folder name, run:

```python
import os
os.listdir("/content/datasets")
```

---

### ⚠️ Important:

* Don’t forget to save the changes to `data.yaml` before training.
* You can edit this file directly in Google Colab using the file browser or with Python like this:

```python
with open('/content/datasets/dottttta1.0-9/data.yaml', 'r') as f:
    content = f.read()
print(content)  # check current paths
```
---













