# Public Model Artifacts 

A centralized, public storage hub for pre-trained model weights and ONNX artifacts used across different projects.

## Overview
This repository serves as a distributed "Asset Store." By hosting heavy binary files (like ONNX models) here as **GitHub Release Assets**, we keep our private code repositories lightweight, fast to clone, and free of massive Git LFS blobs.

## How to Add a New Model
When I have a new project or a new version of a model, follow these steps to add it to the library:

1. **Tag the Model:** Create a new **GitHub Release** in this repository.
2. **Naming Convention:** Use a clear tag like `project-name-v1.0` (e.g., `image-classifier-v1.1`).
3. **Upload Assets:** Attach your `.onnx`, `.pth`, or `.data` files directly to the release.
4. **Update this README:** Add a new entry to the **Active Model Directory** table above with the specific download links.
5. **Point Your Code:** Update your private project's constants to use the new "Latest" URL.

## How to Use in Code
To ensure "Machine Independence," your project should check for the presence of these files locally and download them if they are missing.

### Example (Python + httpx)
```python
import httpx

# Use the 'latest' redirect to always fetch the most recent version
URL = "[https://github.com/sanch-econ/public-model-artifacts/releases/latest/download/sonics-spectttra-gamma-5s.onnx](https://github.com/sanch-econ/public-model-artifacts/releases/latest/download/sonics-spectttra-gamma-5s.onnx)"

def bootstrap():
    with httpx.stream("GET", URL, follow_redirects=True) as r:
        r.raise_for_status()
        with open("model.onnx", "wb") as f:
            for chunk in r.iter_bytes():
                f.write(chunk)
```

## Active Model Directory

### Song AI Classifier (SSD)
**Current Status:** Stable  
**Project:** `sanch-econ/ai-music-classifier`  
**Description:** ONNX export of the Sonics Spectttra Gamma model (5s window) for Synthetic Song Detection.

| Asset File | Permanent "Latest" Link |
| :--- | :--- |
| `*.onnx` (Structure) | [Download](https://github.com/sanch-econ/public-model-artifacts/releases/latest/download/sonics-spectttra-gamma-5s.onnx) |
| `*.onnx.data` (Weights) | [Download](https://github.com/sanch-econ/public-model-artifacts/releases/latest/download/sonics-spectttra-gamma-5s.onnx.data) |

---

