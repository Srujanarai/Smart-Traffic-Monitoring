Smart Traffic Monitoring is developed using Python, incorporating the YOLOv8
deep learning model for object detection and the OpenCV library for video
processing and visualization. The system is designed to detect, classify, and
count various vehicle types such as cars, motorcycles, buses, and trucks from a
video feed or live camera stream. The methodology includes structured modules
for loading the model, processing video input, performing detection, and
rendering the results.

1. Model and Data Initialization
YOLOv8 Model Loading:
The Ultralytics YOLOv8 small model (yolov8s.pt), pre-trained on the COCO
dataset, is loaded at the beginning. This model supports 80 classes, including
multiple vehicle types. It is accessed using the ultralytics Python package.
Vehicle Class Mapping:
A dictionary is defined to map specific class IDs (2: car, 3: motorcycle, 5: bus, 7:
truck) to their corresponding labels.
Data Structures:
- A set vehicle_ids is used to ensure unique vehicle counting.
- A dictionary vehicle_types is initialized to keep count of each vehicle type.
- An integer vehicle_count tracks the total number of vehicles detected.
