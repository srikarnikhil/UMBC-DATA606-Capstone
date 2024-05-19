# Object Detection Using YOLOv8 and Streamlit

## 1. Title and Author

* **Project Title**: Object Detection Using YOLOv8 and Streamlit
* **Prepared for**: UMBC Data Science Master Degree Capstone by Dr. Chaojie (Jay) Wang
* **Author**: Srikar Nikhil Vanama
* **GitHub Profile**: [Srikar Nikhil Vanama](https://github.com/srikarnikhil)
* **LinkedIn Profile**: [Srikar Nikhil Vanama](https://www.linkedin.com/in/srikarnikhil)
* **PowerPoint Presentation**: [Link to Presentation](link_to_presentation)
* **YouTube Video**: [Link to YouTube Video](link_to_youtube_video)

## 2. Background

### What is it about?
This project focuses on using the YOLOv8 model for object detection, a crucial task in computer vision where objects within an image are identified and localized.

### Why does it matter?
Object detection has numerous applications such as surveillance, autonomous driving, and image search, making it an essential technology in various industries.

### Research Questions
1. How effective is the YOLOv8 model in detecting objects in diverse and complex images?
2. Can YOLOv8 be integrated into a web application for real-time object detection?

## 3. Data

### Data Sources
- **COCO Dataset**: [COCO Dataset](https://cocodataset.org/)

### Data Size
- Training images: ~5,922
- Validation images: ~1,000

### Data Shape
- **Training Set**: 5,922 images
- **Validation Set**: 1,000 images

### Time Period
The dataset is not time-bound.

### Representation
Each row represents an image with annotations for various objects within the image.

### Data Dictionary

* **images:**
    * `file_name`: String containing the image file name (e.g., "000000000139.jpg").
    * `height`: Integer representing the pixel height of the image.
    * `width`: Integer representing the pixel width of the image.
    * `id`: Unique integer identifier for the image.

* **annotations:**
    * `bbox`: A list of 4 integers representing the bounding box coordinates in the format `[x, y, width, height]`, where `x` and `y` are the top-left coordinates, and `width` and `height` define the size of the box.
    * `category_id`: Integer ID representing the category of the object (corresponding to the IDs defined in the `categories` section).
    * `image_id`: Integer ID referencing the image to which this annotation belongs.
    * `id`: Unique integer identifier for this annotation.
    * `iscrowd`: Binary value (0 or 1) indicating whether the annotation refers to a single object (0) or a group of objects (1).
    * `segmentation`: (Optional) A list of lists containing the polygon coordinates defining the object's segmentation mask.

* **categories:**
    * `supercategory`: String representing a broader category grouping (e.g., "vehicle").
    * `id`: Unique integer ID for the object category.
    * `name`: String representing the specific object category name (e.g., "car").
 
### Example
  ```json
{
  "images": [
    {"file_name": "000000000139.jpg", "height": 427, "width": 640, "id": 139}
  ],
  "annotations": [
    {"bbox": [263, 85, 95, 222], "category_id": 1, "image_id": 139, "id": 964, "iscrowd": 0}
  ],
  "categories": [
    {"supercategory": "person", "id": 1, "name": "person"}
  ]
}
```

### Target Variable
- The target variable is the bounding box coordinates for object detection.

### Features
- Image data and associated annotations (bounding boxes, object categories).

## 4. Exploratory Data Analysis (EDA)

- **Summary Statistics:**

| Metric                          | Value |
| :-------------------------------- | ----: |
| Number of training images        |  5922 |
| Number of validation images      |  1000 |
| Number of objects in training set | 43458 |
| Number of objects in validation set|  7155 |
| Number of object categories       |    80 |

These statistics reveal insights into the scale and distribution of our dataset, informing our model training strategy and validation procedures.

- **Visualizations:** Bounding boxes were drawn on sample images using the Python Imaging Library (PIL) to visually verify the accuracy of the annotations provided in the COCO dataset. This step allowed for the identification of potential errors in the annotations and confirmed the proper mapping of objects to their respective bounding boxes.


## 5. Model Training

### Models Used
- YOLOv8 model for object detection.

### Training Process
- **Train/Test Split**: The actual dataset already has the train and validation split, which was subsetted later.
- **Python Packages**: Ultralytics YOLOv8, PyTorch, OpenCV, PIL.
- **Development Environment**: Google Colab.

### Performance Metrics
- **Precision, Recall, mAP@0.50, mAP@0.50:0.95, Fitness**: Evaluated over 50, 100, and 171 epochs.

  ### Training Metrics:

| Epochs | Precision | Recall | mAP@0.50 | mAP@0.50:0.95 | Fitness |
|---|---|---|---|---|---|
| 50     | 0.571     | 0.458   | 0.503    | 0.358         | 0.372   |
| 100    | 0.617     | 0.492   | 0.562    | 0.416         | 0.431   |
| 171    | 0.469     | 0.308   | 0.340    | 0.222         | 0.234   |


### Validation Metrics:

| Epochs | Precision | Recall | mAP@0.50 | mAP@0.50:0.95 | Fitness |
|---|---|---|---|---|---|
| 50     | 0.674     | 0.404   | 0.494    | 0.353         | 0.367   |
| 100    | 0.609     | 0.512   | 0.577    | 0.431         | 0.445   |
| 171    | 0.402     | 0.32    | 0.343    | 0.222         | 0.234   |


## Discussion of Results and Limitations

The model's performance, while promising, reveals certain limitations attributed to constraints in computational resources. Due to the computational demands of training YOLOv8, the model was trained on a limited subset of the COCO dataset, consisting of 6000 training images and 1000 validation images. Attempts to train on larger datasets unfortunately led to Google Colab session crashes.

Despite this limitation, we observed an initial improvement in performance metrics (precision, recall, mAP) with an increasing number of epochs, suggesting the model's capacity to learn effectively from the available data. However, early stopping was triggered after 171 epochs, indicating the onset of overfitting and diminishing returns from further training.

The optimal performance was achieved at 100 epochs, demonstrating a balance between model complexity and generalization capability. While the precision of 0.61 may appear modest, the model exhibited commendable object detection accuracy in video analysis.

This suggests that with access to more powerful hardware or distributed training resources, the model could be trained on significantly larger datasets, potentially leading to substantial improvements in its detection capabilities. 



## 6. Application of the Trained Models

### Web Application
- Developed using Streamlit for easy deployment and user interaction.
- Features include object detection on images and videos, with future plans for live camera feed integration.
- 
## Web Application Features

Our web application, developed using Streamlit, leverages the YOLOv8 model and OpenCV to provide robust object detection capabilities. Below are the key features:

### 1. User-Friendly Interface
- **Image and Video Upload**: Users can upload images or videos in various formats (png, jpg, jpeg, mp4).
- **Object Selection**: Allows users to select specific objects to detect from a list of predefined classes. If no objects are selected, the app defaults to detecting all classes.

### 2. Customizable Detection Parameters
- **Confidence Score Slider**: Users can set a minimum confidence score to filter detections, ensuring only high-confidence objects are highlighted.

### 3. Real-Time Processing
- **Image Detection**: Upon uploading an image, the app processes it and displays the detected objects with bounding boxes and labels directly on the image.
- **Video Detection**: For video uploads, the app processes each frame to detect objects, annotating them with bounding boxes and labels, and outputs a processed video.

### 4. Advanced Processing Capabilities
- **Bounding Box Drawing**: Uses OpenCV to draw bounding boxes around detected objects, enhancing visual clarity.
- **Labeling**: Annotates objects with their class names and confidence scores.

These features make the application versatile and user-friendly, suitable for various object detection tasks in both images and videos.

---

Make sure to replace placeholders with actual links to your GitHub profile, LinkedIn profile, presentation, and YouTube video as needed.


## 7. Conclusion

### Summary
The project successfully demonstrated the application of YOLOv8 for object detection, creating a web app for interactive use.

### Limitations
- Limited computational resources restricted the use of the full dataset.
- Further optimization and model tuning are necessary for real-world deployment.

### Lessons Learned
Crucial Role of Dataset Curation: A high-quality, well-annotated dataset is the foundation for successful object detection model training. Thorough data cleaning to remove duplicates and errors, along with careful organization for streamlined data loading, are essential.

Early Stopping and Overfitting: Vigilant monitoring of validation metrics during training is crucial to identify the optimal stopping point and mitigate the risk of overfitting. Even with a relatively small dataset, overfitting can occur, leading to a decline in performance on unseen data.

Balance Between Training Data and Computational Resources:  Training a complex model like YOLOv8 on large datasets requires substantial computational power. Balancing dataset size with available resources is essential to avoid issues like session crashes.

Understanding Validation Metrics: Analyzing validation metrics (precision, recall, mAP) provides a comprehensive view of a model's performance beyond just the F1 score. Careful interpretation of these metrics can guide decisions about model selection and training duration.

### Future Research
- Training with a larger dataset.
- Enhancing the web app with real-time video feed capabilities.

## 8. References

- YOLOv8 Paper: Chien-Yao Wang, Alexey Bochkovskiy, Hong-Yuan Mark Liao
- YOLOv7: Evolving YOLO for Object Detection [arXiv:2207.02696](https://arxiv.org/abs/2207.02696)
- Ultralytics YOLOv8: [Ultralytics YOLOv8 GitHub repository](https://github.com/ultralytics/yolov8)
- Ultralytics Docs: [Ultralytics YOLOv8 official documentation](https://docs.ultralytics.com)

---

Thank you
