# 🔍 Embedding-Based Surface Defect Detection using Qdrant

An end-to-end **industrial defect similarity search system** that helps factories identify surface defects, retrieve similar historical cases, and recommend repair SOPs using **image embeddings + vector search** — fully **offline**, **free**, and with **no paid APIs**.

---

## 📌 Problem Statement

Manufacturing plants generate large volumes of defect images (scratches, cracks, corrosion, etc.). Traditional inspection makes it difficult to:

- Find **visually similar historical defects**
- Reuse **repair knowledge**
- Analyze defects by **severity, shift, or production line**
- Act quickly with **clear repair SOPs**

This project addresses these challenges using **image embeddings** and **Qdrant vector search**.

---

## 🧠 Solution Overview

The system works as follows:

1. Converts defect images into **ORB image embeddings**
2. Stores embeddings in **Qdrant (vector database)**
3. Retrieves **visually similar defects**
4. Filters results by **severity** and **shift**
5. Outputs **repair SOP recommendations**

All components run **locally**, without cloud services or paid APIs.

---

## 🏗️ System Architecture

```
Defect Image
     ↓
ORB Feature Extraction
     ↓
Fixed-size Image Embedding (32-dim)
     ↓
Qdrant Vector Database
     ↓
Similarity Search + Metadata Filtering
     ↓
Defect History + Repair SOP Recommendation
```

---

## 📂 Dataset
### Train–Validation Split

- **Training set** is used to generate image embeddings and populate the Qdrant vector database.
- **Validation set** is used as unseen input images to test similarity search and SOP recommendations.

This setup simulates real-world factory deployment where new defect images are compared against historical defect records.


**NEU Surface Defect Dataset (NEU-DET)**  
An international steel surface defect dataset containing six defect classes:

- Crazing  
- Inclusion  
- Patches  
- Pitted Surface  
- Rolled-in Scale  
- Scratches  

Dataset structure:

```
datasets/NEU-DET/train/images/
 ├── crazing/
 ├── inclusion/
 ├── patches/
 ├── pitted_surface/
 ├── rolled-in-scale/
 └── scratches/
```

---

## ⚙️ Tech Stack

- Python 3.9+
- OpenCV (ORB feature extraction)
- NumPy
- Qdrant (local vector database)
- qdrant-client

No GPU required.  
No cloud services.  
No paid APIs.

---

## 📁 Project Structure

```
factory_Defect_detection/
├── datasets/
│   └── NEU-DET/
├── src/
│   ├── generate_embeddings_orb.py
│   ├── store_orb_in_qdrant.py
│   ├── search_defect_orb.py
│   └── sop_rules.py
├── orb_embeddings.json
├── qdrant_data/
├── requirements.txt
└── README.md
```

---

## 🚀 How to Run the Project

### 1️⃣ Create and activate a virtual environment
```bash
python -m venv factory_env
factory_env\Scripts\activate
```

### 2️⃣ Install dependencies
```bash
pip install -r requirements.txt
```

### 3️⃣ Generate image embeddings
```bash
python src/generate_embeddings_orb.py
```

### 4️⃣ Store embeddings in Qdrant
```bash
python src/store_orb_in_qdrant.py
```

### 5️⃣ Run similarity search with SOP recommendations
```bash
python src/search_defect_orb.py
```

---

## ✅ Sample Output

```
Defect type : scratches
Severity    : high
Shift       : night
Image path  : .../scratches_159.jpg

Recommended SOPs:
scratches → Inspect rollers, polish surface, reduce friction
```

---

## 🛠️ SOP Recommendation Logic

Each detected defect type is mapped to a predefined repair SOP:

- **scratches** → Inspect rollers, polish surface, reduce friction  
- **crazing** → Reduce thermal stress and control cooling rate  
- **pitted_surface** → Check corrosion exposure and clean surface  
- **patches** → Inspect material flow and recalibrate machine  
- **inclusion** → Check raw material purity  
- **rolled-in-scale** → Improve descaling before rolling  

---

## 🔎 Why Qdrant?

- Fast **vector similarity search**
- **Offline/local** deployment
- Flexible **metadata-based filtering**
- Production-ready indexing

---

## 🔮 Future Improvements

- CLIP / ViT embeddings
- Automatic defect severity prediction
- Defect clustering and trend analysis
- Auto-SOP generation with LLMs
- Web dashboard

---

## 📜 License

For educational and research purposes.

---

## 🙌 Acknowledgements

- NEU Surface Defect Dataset
- Qdrant open-source community
- OpenCV contributors
