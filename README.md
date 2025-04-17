# CctvBasedLost-Found

📷 CCTV Detection System using Object Embeddings
This project implements a CCTV detection and object recognition system using recorded video footage in the absence of real-time CCTV access. The system processes multiple video recordings, detects objects, extracts embeddings, and stores them for efficient similarity-based image search.

🛠️ Technologies Used
Python

OpenCV – for frame extraction from videos

YOLOv8 (Ultralytics) – for object detection and bounding box annotation

CLIP (OpenAI) – for converting image crops to vector embeddings

MongoDB – for storing vector embeddings along with metadata

FAISS (optional) – for faster similarity search (not yet integrated in current version)

Flask / Streamlit (optional) – for frontend interface (not covered in this notebook)

NumPy, Pandas, OS, and PIL – utility libraries for file and data manipulation

📌 Steps Followed
1. 🎥 Convert Video to Frames
Processed multiple video recordings simulating different CCTV feeds.

Extracted frames at a consistent interval to ensure coverage.

Assigned each frame a corresponding video stream ID.

2. 🟦 Object Detection with YOLOv8
Used YOLOv8 for detecting objects in each frame.

Created two directories:

Annotated Frames – with bounding boxes drawn.

Cropped Objects – individual object crops from each frame.

3. 🔎 Generate CLIP Embeddings
Converted each cropped object image into vector embeddings using CLIP.

These embeddings serve as unique signatures for visual content.

4. 🧠 Store Embeddings in MongoDB
Each object’s embedding, along with metadata (timestamp, frame path, video stream ID), was stored in MongoDB.

Embeddings are stored in array format for efficient retrieval.

5. 🖼️ Query with an Input Image
A query image is passed through CLIP to obtain its embedding.

Compared this query embedding against all stored embeddings in MongoDB using cosine similarity.

6. 📌 Return the Best Match
The system retrieves and displays:

The most similar object image

The timestamp of detection

The frame/video stream number for traceability
