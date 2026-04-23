# Multimodal MRI Segmentation Pipeline with Explainability

```mermaid
flowchart TD

%% ---------- 1. Input ----------
subgraph Input_Stage [1. Input & Ablation Control]
    direction TB
    A["Multimodal MRI Data (T1, T1ce, T2, FLAIR)"] --> B{"Ablation Controller"}
    B -->|Experiment A| B1["Full Suite"]
    B -->|Experiment B| B2["Drop Modality (e.g., No FLAIR)"]
end

%% ---------- 2. Preprocessing ----------
subgraph Preprocessing [2. Medical Imaging Pipeline]
    direction TB
    B1 --> C["Preprocessing: N4 Bias Correction, Co-registration, Z-Score Normalization"]
    B2 --> C
end

%% ---------- 3. Feature Extraction ----------
subgraph Feature_Extraction [3. Modality-Aware Encoding]
    direction LR
    C --> E1["Encoder T1"]
    C --> E2["Encoder T1ce"]
    C --> E3["Encoder T2"]
    C --> E4["Encoder FLAIR"]
end

%% ---------- 4. Fusion ----------
subgraph Fusion_Layer [4. Explainability Core]
    direction TB
    E1 --> F["Gated Cross-Attention Fusion"]
    E2 --> F
    E3 --> F
    E4 --> F

    F --> G1["Modality Weighting (Alpha Scores)"]
    F --> G2["Saliency Mapping (Grad-CAM / Integrated Gradients)"]
end

%% ---------- 5. Output ----------
subgraph Output_Stage [5. Prediction & Analysis]
    direction TB
    F --> H["Segmentation Decoder (3D / Transformer-based)"]
    H --> I["Tumor Mask (WT, TC, ET)"]
    I --> J["Evaluation: Dice, IoU, HD95"]
end

%% ---------- 6. Reporting ----------
subgraph Report_Bridge [6. Diagnostic Feedback]
    direction TB
    G1 --> K["Explainability Report"]
    G2 --> K
    J --> K
end

%% ---------- Styling ----------
style B fill:#f96,stroke:#333,stroke-width:2px
style F fill:#69f,stroke:#333,stroke-width:2px
style K fill:#9f9,stroke:#333,stroke-width:2px
