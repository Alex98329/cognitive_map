# Cognitive Map-Based Vision-Language Navigation
Map-from-Directions: Vision-Language Navigation with Cognitive Map Generated from Natural Language Instructions via Multimodal Scene Alignment

This repository contains the implementation for the AAAI-26 submission titled:  


It includes notebooks for cognitive map construction, visual environment interpretation, alignment, and evaluation using the Touchdown and Map2Seq datasets.

---

## 📁 Repository Structure

```
.
├── notebooks/
│   ├── LMM_V3_GPT_4o_Map2seq.ipynb
|   ├── Headings_coordinates.ipynb
│   ├── Images_environment_Map2seq.ipynb
│   ├── Environment_description.ipynb
│   ├── Clean_data_description_env.ipynb
│   ├── Matching__inc_sem_Dynamic_programing.ipynb
│   ├── Alignment.ipynb
│   └── Gold_path_evaluation_map2seq.ipynb
├── data/
├── outputs/
├── requirements.txt
└── README.md
```

---

## 🧰 Requirements

Install dependencies with:

```bash
pip install -r requirements.txt
```

Key packages:
- `openai`
- `sentence-transformers`
- `networkx`
- `matplotlib`
- `pandas`
- `opencv-python`
- `numpy`

---

## 🧪 Reproducing the Results

### 📊 Pipeline Summary: Input → Run → Output

| Step | Notebook | Input | Run | Output |
|------|----------|-------|-----|--------|
| 1️⃣ | `OK_LMM_V3_GPT_4o_Map2seq.ipynb` | Navigation instructions (`*.json` from Map2Seq/Touchdown) | GPT-4o parses instructions to generate graph | `dev_graph_lmm.json` (Cognitive Map) |
| 🔁 | `Headings_coordinates.ipynb` | GSV metadata | Manage and process headings | `coordinates.csv`, etc. |
| 2️⃣ | `OK_Images_environment_Map2seq.ipynb` | Waypoints (lat/lon), headings | Fetch and stitch panoramic images | Folder with stitched GSV images |
| 3️⃣ | `OK_environment_description.ipynb` | GSV images (from Step 2) | GPT-4 Vision generates scene descriptions | `raw_environment_descriptions.json` |
| 3.5️⃣ | `OK_clean_data_description_env.ipynb` | Raw scene descriptions (`raw_environment_descriptions.json`) | Clean and normalize descriptions | `cleaned_environment_descriptions.json` |
| 4️⃣ | `OK_matching__inc_sem_Dynamic_programing.ipynb` | Cognitive Map + Cleaned Visual Descriptions | Align via SBERT and Dynamic Programming | `matched_nodes.json`, `alignment_scores.json` |
| 5️⃣ | `OK_Alignment.ipynb` | Cognitive Map + Visual Alignments | Merge aligned nodes into final graph | `final_matched_graph.json` |
| 6️⃣ | `OK_Gold_path_evaluation_map2seq.ipynb` | Predicted paths vs. gold paths | Evaluate navigation success | TC, KPA, SPD scores + visual plots |

---

## 🔑 API Keys Required

This project requires two external APIs:

### 1. OpenAI API Key
Used in:
- `LMM_V3_GPT_4o_Map2seq.ipynb` – for instruction parsing (GPT-4o)
- `Environment_description.ipynb` – for image interpretation (GPT-4 Vision)

Set your key:
```python
import openai
openai.api_key = "your_openai_api_key"
```

### 2. Google Street View Static API Key
Used in:
- `Images_environment_Map2seq.ipynb`
- `Visual_environment_map2seq.ipynb`

You must enable the **Street View Static API** in your [Google Cloud Console](https://console.cloud.google.com/), and set your key:
```python
GSV_API_KEY = "your_google_maps_api_key"
```

The API will fetch panoramic images using:
```
https://maps.googleapis.com/maps/api/streetview
```

## 📄 Notes

- Requires **OpenAI API key** for GPT-4o / Vision.
- Ensure consistent file paths and `outputs/` folder structure.
- Tested with Python 3.10 and NVIDIA GPU.
- For reproducibility of the AAAI-26 submission, please refer to Release v1.0.
---

## 📜 License

MIT License

