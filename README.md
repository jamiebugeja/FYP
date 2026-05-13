# A Multimodal AI Approach to Analysing Nationality Representation in Maltese Online News

This repository contains the implementation for a Final Year Project (FYP) that investigates how nationalities are represented in Maltese online news using a multimodal Artificial Intelligence approach. The system combines Natural Language Processing (NLP) and Computer Vision (CV) methods to analyse both article text and accompanying images.

The project was developed as part of the Bachelor of Science in Information Technology (Honours) in Artificial Intelligence.

## IMPORTANT NOTE

Due to their large sizes, both sentiment models were not uploaded to this repository. 
Therefore, they can be accessed and downloaded into this repository by navigating to the [Sentiment Model Google Drive](https://drive.google.com/drive/folders/12YXblQ_mOsWgUnFTRHsviV-9L3p3EWKG?usp=drive_link)


## Project Overview

News representation is shaped by both written content and visual material. This project therefore analyses nationality representation using two complementary pipelines:

1. **Textual Analysis Pipeline**
   - Extracts nationality mentions from Maltese online news articles.
   - Maps nationality mentions to ISO3 country codes.
   - Applies sentiment analysis at article and mention level.
   - Applies framing analysis using predefined media frames.

2. **Visual Analysis Pipeline**
   - Extracts article images.
   - Detects people in images using YOLOv8.
   - Detects faces within person detections.
   - Applies exploratory face attribute estimation.
   - Computes visibility-related features such as shot type, crowding, and prominence.

The outputs from both pipelines are then combined in a multimodal analysis to compare textual portrayal with visual presentation.

## Main Research Aim

The aim of this project is to provide a data-driven analysis of nationality representation in Maltese online news by examining how nationalities are mentioned, framed, and visually represented across article text and images.

## Repository Structure

```text
FYP Project/
├─ Data/
│  ├─ Articles/
│  │  ├─ Output/
│  │  │  ├─ Articles_eval_mentions_summary.csv
│  │  │  ├─ Articles_merged_enriched.csv
│  │  │  ├─ Articles_merged_mentions.csv
│  │  │  ├─ Articles_nationalities_enriched.csv
│  │  │  ├─ Articles_pattern_rule_mentions.csv
│  │  │  ├─ Articles2024_labelled_enriched.csv
│  │  │  └─ Articles2024_labelled_mentions.csv
│  │  ├─ Articles2024.csv
│  │  ├─ Articles2025.csv
│  │  ├─ Articles2024_batch_labelled.csv
│  │  └─ Articles2024_mentions_sampled_labelled.csv
│  ├─ Images/
│  │  ├─ Output/
│  │  │  ├─ annotated_images/    # Not Uploaded due to large size
│  │  │  ├─ person_detections.csv
│  │  │  ├─ article_image_text_mapping.csv
│  │  │  └─ person_detections_with_face_attributes.csv
│  │  └─ Plain_Images/     # Not Uploaded due to large size
├─ sentiment_finetuned_xlmr/     # Not Uploaded due to large size, download from google drive link above
├─ sentiment_finetuned_xlmr_mentions/     # Not Uploaded due to large size, download from google drive link above
├─ extract_images_from_articles.ipynb
├─ samples_training_evaluation.ipynb
├─ textual_pipeline.ipynb
├─ visual_pipeline.ipynb
├─ multimodal_analysis.ipynb
├─ requirements.txt
├─ yolov8m.pt
└─ README.md
```

## Main Notebooks

### `textual_pipeline.ipynb`

Runs the textual modality of the system. It extracts nationality mentions, applies sentiment analysis, performs framing analysis, and generates article-level and mention-level outputs.

### `extract_images_from_articles.ipynb`

Extracts article images from the dataset and stores them in the expected image directory. This notebook should be run before the visual pipeline.

### `visual_pipeline.ipynb`

Runs the visual modality of the system. It performs person detection, face detection, face attribute estimation, visibility analysis, and optional image annotation.

### `multimodal_analysis.ipynb`

Combines the outputs of the textual and visual pipelines. It produces multimodal results linking article sentiment and framing with visual features such as visibility, crowding, and model-estimated race categories.

### `samples_training_evaluation.ipynb`

Used to prepare labelled samples, fine-tune the sentiment models, and evaluate their performance. This is only needed if the sentiment models are being retrained.

## Installation

Create a Python environment and install the required dependencies:

```bash
pip install -r requirements.txt
```

The project was developed using Python and IPython Notebook files. Main libraries include:

- pandas
- numpy
- spaCy
- Hugging Face Transformers
- PyTorch
- Ultralytics
- OpenCV
- DeepFace
- pycountry

The textual pipeline also requires the spaCy transformer model:

```bash
python -m spacy download en_core_web_trf
```

## Execution Order

To reproduce the full project workflow, run the notebooks in the following order.

### 1. Run the textual pipeline

```text
textual_pipeline.ipynb
```

This performs nationality extraction, sentiment analysis, framing analysis, and textual result generation.

### 2. Extract article images

```text
extract_images_from_articles.ipynb
```

This extracts images from the article dataset and saves them in the expected image folder.

### 3. Run the visual pipeline

```text
visual_pipeline.ipynb
```

This performs person detection, face detection, face attribute estimation, visibility analysis, and annotation generation.

### 4. Run the multimodal analysis

```text
multimodal_analysis.ipynb
```

This merges textual and visual outputs and produces the final multimodal results.


## Multimodal Analysis

The multimodal stage combines textual and visual outputs using article identifiers. This allows the project to examine relationships between:

- Article sentiment and detected visual groups
- Article framing and visual representation
- Crowding and article tone
- Visibility and article tone
- Model-estimated race categories and textual framing

These results are intended to support aggregate-level analysis of patterns in Maltese online news representation.

## Important Ethical Note

This project analyses socially sensitive categories, including nationality and race-like visual attribute estimation. The outputs should be interpreted carefully.

Nationality mentions are based on article text and should be treated as indicators of media portrayal, not as complete descriptions of individuals. Similarly, face attribute estimation is exploratory and should not be treated as a factual classification of a person’s identity.

The visual race categories are model-estimated outputs from a pre-trained system. They may be affected by model bias, image quality, lighting, blur, pose, face size, and dataset imbalance. These outputs are used only for aggregate exploratory analysis.


## Author

Jamie Bugeja  
Bachelor of Science in Information Technology (Honours) in Artificial Intelligence  
Final Year Project, May 2026

## Supervisor

Dr Dylan Seychell

## Disclaimer

This project is intended for academic research purposes. The results should be interpreted as indicators of representational patterns in the dataset, not as proof of editorial intent or factual identity classification.
