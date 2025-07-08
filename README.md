# Smart-Traffic-Monitoring
The system identifies multiple types of vehicles—such as cars, trucks, buses, and motorcycles—and counts them as they cross a predefined virtual line in the video frame.

Smart Traffic Monitoring is developed using Python, incorporating the YOLOv8 deep learning model for object detection and the OpenCV library for video processing and visualization. The system is designed to detect, classify, andcount various vehicle types such as  cars,motorcycles, buses, and trucks from a video feed or live camera stream. The methodology includes structured modules for loading the model, processing video input, performing detection, and rendering the results.
1. Model and Data Initialization
YOLOv8 Model Loading:
The Ultralytics YOLOv8 small model (yolov8s.pt), pre-trained on the COCO dataset, is loaded at the beginning. This model supports 80 classes, including multiple vehicle types. It is accessed using the ultralytics Python package.
Vehicle Class Mapping:
A dictionary is defined to map specific class IDs (2: car, 3: motorcycle, 5: bus, 7: truck) to their corresponding labels.
Data Structures:
 A set vehicle_ids is used to ensure unique vehicle counting.
 A dictionary vehicle_types is initialized to keep count of each vehicle type.
 An integer vehicle_count tracks the total number of vehicles detected.
2. Video Frame Processing
Video Input:
The program uses OpenCV’s cv2.VideoCapture() to load the video file (or webcam stream). Frames are read one at a time using a loop, and detection is performed on each frame.
Counting Line Definition:
A fixed horizontal line (at line_y = 300) is drawn across the frame. Vehicles are counted only when their center crosses this line within a margin range (±20 pixels).
3. Detection and Classification Logic
Object Detection:
Each frame is passed to the YOLOv8 model using the .predict() method. Detected bounding boxes are returned along with class IDs and confidence scores.
Class Filtering:
Only detections with class IDs that match predefined vehicle types are processed further.

Bounding Box Handling:
 Bounding box coordinates (x1, y1, x2, y2) are used to calculate the center point of the vehicle.
 This center point is checked against the virtual line to determine if the vehicle should be counted.
4. Vehicle Counting Algorithm
Unique Counting Strategy:
 To avoid multiple counts of the same vehicle, a tuple (center_x,vehicle_type) is stored in the vehicle_ids set.
 A vehicle is counted only once when its center crosses the counting line for the first time.
Count Incrementation:
 On valid crossing, both vehicle_count and the specific vehicle type count in vehicle_types are incremented.
5. Visual Output and Interface Drawing Bounding Boxes:
 A blue rectangle is drawn around each detected vehicle.
 Labels show vehicle type and confidence score (e.g., "Car
(0.87)"). Drawing Counting Line:
 A green line is overlaid across the video frame at the counting level. Overlay Display:
 A semi-transparent black rectangle is drawn at the top of the frame to display real-time statistics.
Text Display:
 cv2.putText() is used to render total vehicle count and individual counts
for each type.
6. Real-time Interaction and Exit Live Display:
 Each processed frame is shown in a window titled “Vehicle Detection & Counting”.
 Exit Option:
 The program allows the user to press 'q' to stop the video and exit the loop gracefully.
7. Validation and Constraints Confidence Threshold:
 A confidence threshold of 0.3 is set to filter out low-confidence detections, improving result reliability.
Class Validation:
 Only COCO vehicle classes (car, truck, motorcycle, bus) are processed. Line Margin:
 A margin range (±20 pixels) is applied around the counting line to account for minor shifts in vehicle center positions.
Frame Read Errors:
 If a frame cannot be read, the system exits gracefully and prints a message.
8. Error Handling and Debugging
Debug Statements:
 Print statements are included to log detected vehicles, class names, and their confidence levels.
 Trucks and specific detections can be logged with additional messages for deeper debugging.
Final Summary:
 At the end of the video, a complete summary is printed to the console,listing the total number of vehicles and the count for each type.

