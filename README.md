# Transfer Learning Project: Guava Disease Classification

This project is part of a series exploring the effective use of **transfer learning** on small 
datasets. The focus of this project is to demonstrate the importance of using the proper pretrained 
model weights before fine-tuning for specific tasks. This project focuses on the classification 
of guava disease types using transfer learning with the **VGG19** architecture pretrained on different 
weights.

## Project Workflow

### 1. **Dataset Preparation**
The dataset, `GuavaDiseaseDataset`, is organized into three directories: 
`train`, `val`, and `test`. Images are resized to `224x224` and augmented using `ImageDataGenerator`.

#### Key Steps:
- **Dataset Shrinking**: To limit dataset size for simulation of limited data scenarios.
- **Data Augmentation**:
  - Rescaling pixel values.
  - Applying rotations, zooms, flips, and shearing.

### 2. **Model Architectures**
Three different pretrained VGG19 models were tested, each fine-tuned for the guava disease 
classification task.

#### Model Variants:
1. **Imagenet Pretrained VGG19**  
   Used pretrained weights from ImageNet and added custom dense layers for classification.
   
2. **Fruits and Vegetables VGG19**  
   A model pretrained on classifying fruits and vegetables , fine-tuned for guava disease classification.

3. **Brain Tumor VGG19**  
   A model pretrained on detecting and classifying brain tumors, fine-tuned for guava disease 
classification.

### 3. **Training and Fine-Tuning**
- Initially, only the added dense layers were trainable, with the pretrained layers frozen.
- Fine-tuning involved unfreezing the pretrained layers and training with a lower learning rate (`1e-5`).
- Early stopping was employed to prevent overfitting.

### 4. **Evaluation**
- Evaluated each model on the test dataset.
- Metrics:
  - **Accuracy**: Model classification accuracy.
  - **Loss**: Cross-entropy loss.

### 5. **Visualization**
- Plotted accuracy and loss trends using `plot_accuracy()` and `plot_loss()`.
- Final metrics were summarized with `summarize_final_metrics()`.

### Key Python Files
- `utils.py`: Contains utility functions for dataset shrinking, visualization, and performance summaries.

### Results
Each model's performance was compared to determine how well the pretrained weights contributed to 
guava disease classification.

#### Metrics:
| Model                     | Accuracy | Loss |
|---------------------------|----------|------|
| Imagenet Pretrained VGG19 | 95.8%    | 0.73 |
| Fruits & Vegetables VGG19 | 67.1%    | 0.98 |
| Brain Tumor VGG19         | 91.8%    | 0.91 |

### Findings:

The architecture for all those models was the exact same, taking VGG19 as the base and simply changing 
the starting weights.

- The **Imagenet VGG19** model provides the best performance, being a great multipurpose pretrained 
- model that is easy to fine tune on different datasets.


- The **Fruits and Vegetables VGG19** model, although pretrained on classifying fruits and vegetables, 
did not perform as well as the other models. This might be due to how much it relied on higher level
features to classify fruits, focusing more on less detailed information.


- The **Brain Tumor VGG19** model, although pretrained on detecting and classifying brain tumors,
performed quite well. Although this is an odd choice of pretrained weights for guava disease 
classification, but it focuses more on finding anomolies in more detailed information, taking lower 
layers into stronger account. This explains the surprisingly good performance on our mode.