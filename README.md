# Cognitive Map-Based Vision-Language Navigation
Map-from-Directions: Vision-Language Navigation with Cognitive Map Generated from Natural Language Instructions via Multimodal Scene Alignment

# Cognitive Map-Based Vision-Language Navigation

This repository contains the implementation for the AAAI-26 submission titled:  
**"Cognitive Map Generation from Natural Language Instructions via Multimodal Scene Alignment"**

It includes notebooks for cognitive map construction, visual environment interpretation, alignment, and evaluation using the Touchdown and Map2Seq datasets.

---

## 📁 Repository Structure

```
.
├── notebooks/
│   ├── OK_LMM_V3_GPT_4o_Map2seq.ipynb
│   ├── OK_Images_environment_Map2seq.ipynb
│   ├── OK_environment_description.ipynb
│   ├── OK_clean_data_description_env.ipynb
│   ├── OK_matching__inc_sem_Dynamic_programing.ipynb
│   ├── OK_Alignment.ipynb
│   └── OK_Gold_path_evaluation_map2seq.ipynb
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
| 2️⃣ | `OK_Images_environment_Map2seq.ipynb` | Waypoints (lat/lon), headings | Fetch and stitch panoramic images | Folder with stitched GSV images |
| 3️⃣ | `OK_environment_description.ipynb` | GSV images (from Step 2) | GPT-4 Vision generates scene descriptions | `raw_environment_descriptions.json` |
| 3.5️⃣ | `OK_clean_data_description_env.ipynb` | Raw scene descriptions (`raw_environment_descriptions.json`) | Clean and normalize descriptions | `cleaned_environment_descriptions.json` |
| 4️⃣ | `OK_matching__inc_sem_Dynamic_programing.ipynb` | Cognitive Map + Cleaned Visual Descriptions | Align via SBERT and Dynamic Programming | `matched_nodes.json`, `alignment_scores.json` |
| 5️⃣ | `OK_Alignment.ipynb` | Cognitive Map + Visual Alignments | Merge aligned nodes into final graph | `final_matched_graph.json` |
| 6️⃣ | `OK_Gold_path_evaluation_map2seq.ipynb` | Predicted paths vs. gold paths | Evaluate navigation success | TC, KPA, SPD scores + visual plots |

---

## 📝 Notes

- You need an **OpenAI API key** to access GPT-4o and GPT-4 Vision capabilities.
- Ensure image input/output paths are consistent across notebooks.
- The system was tested using Python 3.10 and a single GPU.

---

## 📜 License

MIT License
