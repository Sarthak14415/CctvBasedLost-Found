# CctvBasedLost-Found

# 📷 CCTV Detection System using Object Embeddings

This project implements a CCTV detection and object recognition system using recorded video footage in the absence of real‑time CCTV access. The system processes multiple video recordings, detects objects, extracts embeddings, and stores them for efficient similarity‑based image search.

---

## 🛠️ Technologies Used

- **Python**  
- **OpenCV** – for frame extraction from videos  
- **YOLOv8 (Ultralytics)** – for object detection and bounding‑box annotation  
- **CLIP (OpenAI)** – for converting image crops to vector embeddings  
- **MongoDB** – for storing vector embeddings along with metadata  
- **FAISS** *(optional)* – for faster similarity search (not yet integrated)  
- **Flask / Streamlit** *(optional)* – for frontend interface (not covered in this notebook)  
- **NumPy, Pandas, OS, PIL** – utility libraries for file and data manipulation  

---

## 📌 Steps Followed

1. 🎥 **Convert Video to Frames**  
   - Process multiple video recordings simulating different CCTV feeds.  
   - Extract frames at a consistent interval to ensure coverage.  
   - Assign each frame a corresponding video‑stream ID.  

2. 🟦 **Object Detection with YOLOv8**  
   - Load and run the YOLOv8 model to detect objects in each frame.  
   - Save outputs to two directories:  
     - **`annotated_frames/`** – frames with bounding boxes drawn  
     - **`cropped_objects/`** – individual object crops from each frame  

3. 🔎 **Generate CLIP Embeddings**  
   - Feed each cropped object image into the CLIP model to extract a fixed‑length embedding vector.  
   - Use these embeddings as unique signatures for visual content.  

4. 🧠 **Store Embeddings in MongoDB**  
   - Convert PyTorch tensors to lists and store embeddings in MongoDB via PyMongo.  
   - Include metadata: timestamp, frame path, and video‑stream ID.  

5. 🖼️ **Query with an Input Image**  
   - Encode a user‑provided query image with CLIP to produce its embedding.  
   - Compute cosine similarity between the query embedding and all stored embeddings.  

6. 📌 **Return the Best Match**  
   - Retrieve and display:  
     - The most similar object image  
     - The detection timestamp  
     - The corresponding frame/video‐stream number  

---
## 📚 Technologies by Step

Below is a step‑by‑step breakdown of the libraries, frameworks, and tools used in each phase of the CCTV detection system:

### 1. Convert Video to Frames
- **Language & Environment**: Python  
- **Core Library**:  
  - OpenCV (`cv2`)  
- **Utilities**:  
  - `os` / `pathlib` for filesystem operations  
  - `tqdm` for progress bars  

### 2. Object Detection with YOLOv8
- **Model & API**:  
  - Ultralytics YOLOv8 (`from ultralytics import YOLO`)  
- **Image I/O & Drawing**:  
  - OpenCV (`cv2.imread`, `cv2.rectangle`, `cv2.imwrite`)  
  - PIL (`from PIL import Image`) for format conversions  

### 3. Generate CLIP Embeddings
- **Model**:  
  - OpenAI CLIP (`import clip`)  
- **Framework**:  
  - PyTorch (`import torch`)  
- **Preprocessing**:  
  - `clip.load` & `clip.tokenize` transforms  
  - `torchvision.transforms` for image resizing & normalization  

### 4. Store Embeddings in MongoDB
- **Database**:  
  - MongoDB  
- **Driver**:  
  - PyMongo (`from pymongo import MongoClient`)  
- **Data Handling**:  
  - Convert tensors to lists (`.cpu().numpy().tolist()`)  
  - Store embeddings alongside metadata (timestamp, frame path, stream ID)  

### 5. Query Embedding & Similarity Search
- **Query Processing**:  
  - CLIP + PyTorch stack (same as Step 3)  
- **Similarity Calculation**:  
  - NumPy (`import numpy as np`)  
  - `sklearn.metrics.pairwise.cosine_similarity` (or manual dot‑product)  

### 6. Return & Display Results
- **Result Formatting**:  
  - Python standard I/O (e.g. `print`) or simple web rendering (Flask / Streamlit)  
- **Metadata Lookup**:  
  - MongoDB queries via PyMongo to fetch timestamp, stream ID, and image path  

---
