# DetectNode Example Models

This repository contains a collection of third-party, publicly available machine learning models aggregated from various open-source projects for demonstration, testing, and comparative purposes with the DetectNode app. 

> **Note:** None of the models hosted here were originally created or trained by me. All rights, copyrights, and original works belong to their respective authors and organizations.

---

The `yolov5m_artpec` models come from the [Axis Model Zoo](https://github.com/AxisCommunications/axis-model-zoo) and run on the DLPU. 
The other models run on the camera CPU using ONNX Runtime. This is not an officially supported way of loading a model, but it supports a broader set of operators than TFLite.
Depending on the hardware and how many apps are running, loading an ONNX model might crash the camera.

| Model             | Platform / Target | Average Inference Speed | Download                                                                                                     |
| :---------------- | :---------------- | :---------------------- | :----------------------------------------------------------------------------------------------------------- |
| `yolov5m_artpec8` | Axis ARTPEC-8     | 210 ms (P3265)          | [Download](https://github.com/DetectNode/example-models/releases/download/v1.0.0/yolov5m_artpec8.detectnode) |
| `yolov5m_artpec9` | Axis ARTPEC-9     | 85 ms (P3275)           | [Download](https://github.com/DetectNode/example-models/releases/download/v1.0.0/yolov5m_artpec9.detectnode) |
| `yolo26n`         | CPU (ONNX)        | 800 ms (P3275)          | [Download](https://github.com/DetectNode/example-models/releases/download/v1.0.0/yolo26n.detectnode)         |
| `yolo26l`         | CPU (ONNX)        | 7200 ms (P3275)         | [Download](https://github.com/DetectNode/example-models/releases/download/v1.0.0/yolo26l.detectnode)         |
| `skywater_seg`    | CPU (ONNX)        | 4100 ms (P3275)         | [Download](https://github.com/DetectNode/example-models/releases/download/v1.0.0/skywater_seg.detectnode)    |


##  How to Use

1. Download the `.detectnode` package for your model of choice
2. Launch and open the DetectNode app, then click on **"Add scenario"**.
3. Click on **"Add a new model"** and upload your downloaded `.detectnode` file.


##  Model Details & Acknowledgments

### SkyWater-Seg (`skywater_seg`)
* **Author:** Vincent Qin (Realcat)
* **Upstream Repository:** Vincentqyw/skywater
* **License:** MIT
* **Description:** SegFormer MiT-B2 fine-tuned on ADE20K for sky, water, and person segmentation. Designed to pre-filter images for Structure from Motion (SfM) pipelines by masking out dynamic or featureless regions.
* **Performance:** CPU inference only (~4100 ms per frame on P3275). Does not have enough available memory to run on P3265, even though both cameras have 2 GB of RAM.

### YOLO26 Models (`yolo26l`, `yolo26n`)
* **Author:** zwh20081 (Source: Ultralytics)
* **Upstream Repository:** zwh20081/yolo26-onnx
* **License:** AGPL-3.0
* **Description:** Object detection models in ONNX format (opset 12), optimized for CPU/GPU inference via ONNX Runtime at $640 \times 640$ resolution.
* **Performance:** Run on the camera CPU (no DL-LPU acceleration), so they are slow and memory-hungry. Mainly useful for testing and comparison.

### Axis ARTPEC Models (`yolov5m_artpec8`, `yolov5m_artpec9`)
* **Author:** Axis Communications AB
* **Upstream Repository:** Axis Model Zoo
* **License:** AGPL-3.0-only (Model Weights) / Apache-2.0 (Upstream Code/Tools)
* **Description:** Object detection models (YOLOv5m) optimized and compiled specifically for Axis network cameras running on ARTPEC-8 and ARTPEC-9 chips.
* **Performance:** ≈85 ms average inference on P3275 and ≈210 ms on P3265. These run on the DL-LPU and are the recommended models for live detection.

## License & Legal Notice

All model packages retain their original open-source license agreements. A copy of the respective license and configuration metadata is included inside each model directory and `.detectnode` archive.

* **YOLOv5 & YOLO26 Models:** To comply with Ultralytics licensing terms, model weight files are licensed under AGPL-3.0-only.
* **SkyWater-Seg:** Distributed under the MIT License.
* **Axis Communications Tooling:** Upstream code and build tools are licensed under Apache-2.0.

Please consult the specific `LICENSE` file located inside each model directory prior to commercial use or redistribution.