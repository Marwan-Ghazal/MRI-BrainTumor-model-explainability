# Multimodal MRI Segmentation Pipeline

```mermaid
flowchart LR
A["Input Layer: Multimodal MRI Data (T1, T2, FLAIR)"] --> B["Preprocessing: Alignment, Normalization, Standardization"]
B --> C["Feature Extraction"]
C --> D["Feature Fusion"]
D --> E["Segmentation Module"]
E --> F["Segmentation Output"]
E --> G["Explainability Module"]
F --> H["Evaluation Module: Quantitative Metrics"]
