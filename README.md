
 Brain Tumor MRI Image Classification Using Deep Learning
This project aims to develop an accurate and efficient deep learning-based solution to classify brain MRI images into four categories: glioma tumor, meningioma tumor, pituitary tumor, and no tumor. Brain tumors are among the most life-threatening forms of cancer, and early, precise detection is critical for effective treatment. Manual diagnosis through MRI scans can be time-consuming and prone to human error due to the complexity and subtlety of tumor features. This project demonstrates how deep learning and transfer learning can be leveraged to build a robust image classification pipeline to support radiologists in making faster, more reliable diagnoses.

1 Data Understanding & Exploration The dataset contains 2,443 labeled brain MRI images, pre-split into training, validation, and test sets. Initial exploration focused on understanding the dataset’s structure, checking for missing values, duplicate entries, and ensuring that image file paths were valid and correctly formatted. Visualizations such as count plots and bar charts were used to assess the distribution of tumor types across dataset splits. This revealed a moderate class imbalance, with glioma tumors being the most frequent and the no tumor category having the fewest samples. Knowing this imbalance early helped shape data augmentation and model training strategies.

2 Data Wrangling & Preprocessing Data cleaning steps included standardizing label formats (lowercasing, trimming whitespaces) and ensuring all file paths used consistent directory structures for smooth image loading. While there were no missing values in this dataset, the workflow accounted for potential imputation if needed. Categorical labels were encoded using one-hot encoding to prepare them for model training. The images were resized and normalized to ensure they matched the input size requirements of the chosen CNN architectures and that pixel values fell within a consistent range for stable gradient updates.

3 Feature Engineering & Visualization To understand relationships within the data, multiple charts were generated — showing class balance, split distributions, and sample images from each class. This helped validate that the dataset was well-prepared for training and that all tumor types were visually distinguishable. No advanced feature extraction was needed since the project relies on Convolutional Neural Networks to learn complex hierarchical features directly from pixel data.

4 Model Development & Comparison Three models were developed and compared:

Model 1: A custom CNN built from scratch, serving as a baseline for comparison.

Model 2: The same CNN architecture with hyperparameter tuning using GridSearchCV and RandomSearchCV to optimize filter sizes, dropout rates, and learning rates.

Model 3: A MobileNetV2 transfer learning model, pre-trained on ImageNet, with a custom classification head fine-tuned on the brain tumor dataset.

The MobileNetV2 model was chosen because transfer learning leverages learned visual features from millions of generic images, which improves feature extraction on small or medium-sized medical datasets.

5 Hyperparameter Tuning & Cross-Validation Keras Tuner’s RandomSearch was used to optimize the MobileNetV2’s dense layer units, dropout rates, and learning rates. This approach was chosen because it efficiently explores a large hyperparameter space without the computational cost of exhaustive grid search. Cross-validation ensured that the model generalized well across different data splits, and results showed a clear improvement in validation accuracy and reduced overfitting compared to the baseline models.

6 Evaluation Metrics & Explainability Performance was evaluated primarily using accuracy and categorical cross-entropy loss, which are appropriate for multi-class classification problems. Additional focus was placed on class-wise performance to ensure minority classes like no tumor were not underrepresented in predictions — crucial in a medical context to avoid dangerous false negatives.

To ensure the model’s predictions are interpretable and trustworthy, Grad-CAM (Gradient-weighted Class Activation Mapping) was applied to generate heatmaps showing which parts of an MRI scan influenced the model’s classification. This step validated that the network focused on the relevant tumor regions rather than unrelated background features, which increases clinicians’ trust in the AI system.

7 Saving & Deployment After evaluation, the best-performing model, MobileNetV2, was saved in .h5 format for easy reuse and deployment in real-world applications. The saved model was reloaded and tested on an unseen MRI image to ensure that the serialization and deserialization pipeline worked correctly, providing consistent predictions after deployment.

8 Business & Social Impact Automating brain tumor detection has significant benefits. By supporting radiologists with fast, consistent, and reliable second opinions, this solution can help reduce diagnostic delays and improve patient outcomes. It minimizes the chance of oversight in complex cases and can be integrated into hospitals’ existing diagnostic workflows. Lightweight models like MobileNetV2 can even be deployed on portable edge devices, making advanced diagnostics more accessible in remote or resource-limited regions.

Conclusion This project showcases a complete deep learning pipeline, from data exploration to preprocessing, model training, hyperparameter tuning, explainability, and deployment readiness. It highlights the power of transfer learning for medical imaging tasks and demonstrates how AI can assist healthcare professionals in delivering better, faster, and more accurate care to patients.
