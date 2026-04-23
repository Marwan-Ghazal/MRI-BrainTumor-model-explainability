# Multimodal MRI Segmentation with Ablation & Explainability

```mermaid
flowchart TD

%% 1. Input & Ablation
subgraph Input_Stage [1. Input & Ablation Control]
A["Multimodal MRI Data (T1, T1ce, T2, FLAIR)"] --> B{"Ablation Controller"}
B -->|Experiment A| B1["Full Suite"]
B -->|Experiment B| B2["Drop Modality (e.g., No FLAIR)"]
end

%% 2. Preprocessing
subgraph Preprocessing [2. Medical Imaging Pipeline]
B1 --> C["Preprocessing: N4 Bias Correction, Co-registration, Z-Score Normalization"]
B2 --> C
end

%% 3. Feature Extraction
subgraph Feature_Extraction [3. Modality-Aware Encoding]
C --> E1["Encoder T1"]
C --> E2["Encoder T1ce"]
C --> E3["Encoder T2"]
C --> E4["Encoder FLAIR"]
end

%% 4. Fusion
subgraph Fusion_Layer [4. Explainability Core]
E1 --> F["Gated Cross-Attention Fusion"]
E2 --> F
E3 --> F
E4 --> F

F --> G1["Modality Weighting (Alpha Scores)"]
F --> G2["Feature Importance (Grad-CAM / Saliency)"]
end

%% 5. Output
subgraph Output_Stage [5. Prediction & Analysis]
F --> H["Segmentation Decoder (Dense Prediction)"]
H --> I["Tumor Mask (WT, TC, ET)"]
I --> J["Evaluation: Dice per region, HD95"]
end

%% 6. Report
subgraph Report_Bridge [6. Diagnostic Feedback]
G1 --> K["Explainability Report"]
G2 --> K
J --> K
end

%% Styling
style B fill:#f96,stroke:#333,stroke-width:2px
style F fill:#69f,stroke:#333,stroke-width:2px
style K fill:#9f9,stroke:#333,stroke-width:2px
