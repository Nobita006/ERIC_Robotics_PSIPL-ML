### Report: Methodology, Model Performance, and Insights

---

#### **Objective**

The objective was to develop a machine learning model to classify images of industrial equipment into two categories: **'defective'** and **'non-defective'**. This involved:
---

#### **Methodology**

1. **Dataset Preparation**:
   - The dataset was organized into two categories: 'defective' and 'non-defective'.
   - Images were dynamically augmented during training to enhance diversity without increasing storage overhead. Augmentation included transformations such as:
     - **Random Rotation**: To handle orientation variance.
     - **Horizontal Flip**: To add diversity.
     - **Resized Crop**: To simulate different equipment views.
     - **Color Jitter**: To account for lighting variations.

2. **Model Selection and Architecture**:
   - **Pretrained ResNet18**: A ResNet18 model pretrained on ImageNet was selected for its robustness and computational efficiency.
   - **Transfer Learning**:
     - The earlier layers of ResNet18 were frozen to retain learned features from ImageNet.
     - The final fully connected layer was modified for binary classification.

3. **Loss Function and Optimization**:
   - **Weighted Cross-Entropy Loss**: To address the class imbalance, weights were assigned inversely proportional to class frequencies.
   - **Adam Optimizer**: Used for its adaptability in updating model weights.

4. **Data Loading and Training**:
   - **Efficient Data Loading**: Configured with `num_workers=4` and `pin_memory=True` to speed up data transfer.
   - **Batch Size**: A batch size of 32 was used to balance memory efficiency and training speed.
   - **Epochs**: The model was trained for 10 epochs with dynamic progress tracking using `tqdm`.

5. **Evaluation Metrics**:
   - Metrics used included **accuracy**, **precision**, **recall**, **F1-score**, and a **confusion matrix** to assess performance on test data.

---

#### **Model Performance**

**Classification Report**:
| Class          | Precision | Recall | F1-Score | Support |
|----------------|-----------|--------|----------|---------|
| Defective      | 0.94      | 0.82   | 0.88     | 126     |
| Non-defective  | 0.95      | 0.99   | 0.97     | 467     |
| **Overall**    | **0.95**  | **0.95**| **0.95** | **593** |

**Confusion Matrix**:
```
[[103  23]
 [  6 461]]
```

- **Accuracy**: 95%
- **Macro Average**:
  - Precision: 95%
  - Recall: 90%
  - F1-Score: 92%
- **Weighted Average**:
  - Precision: 95%
  - Recall: 95%
  - F1-Score: 95%

---

#### **Insights**

1. **Model Strengths**:
   - High accuracy and F1-score (95%) demonstrate the model's robustness.
   - **Non-defective class** achieved exceptional recall (99%), ensuring minimal false negatives, which is crucial for real-world deployment to identify functioning equipment accurately.

2. **Defective Class Recall**:
   - The recall for the defective class was slightly lower (82%). This indicates that the model occasionally misclassifies defective images as non-defective, possibly due to subtle defect features.

3. **Impact of Augmentation**:
   - Dynamic augmentations enriched the dataset diversity, improving the model's ability to generalize to unseen data.

4. **Class Imbalance**:
   - Weighted loss effectively mitigated the class imbalance, ensuring fair treatment of the minority class.

5. **Training Efficiency**:
   - Leveraging transfer learning with ResNet18 significantly reduced training time while maintaining high performance, making the solution computationally efficient for mid-range GPUs.

---

#### **Conclusion**

The project successfully achieved the objective of classifying industrial equipment into 'defective' and 'non-defective' categories with a **95% accuracy**. Leveraging transfer learning, weighted loss, and dynamic augmentations ensured high model performance despite the class imbalance. This methodology provides a robust framework for industrial defect classification and can be extended to other similar applications. 
