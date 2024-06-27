# ADAS-LKAS
# Lane Detection and Drift Correction with YOLO and Kinect

This project aims to detect lane lines and correct vehicle drift using a YOLO object detection model and a Kinect sensor for depth and color streaming. The system provides visual feedback on lane keeping and suggests corrective actions if the vehicle is drifting out of the lane.

## Requirements

- Python 3.x
- OpenCV
- NumPy
- OpenNI
- YOLO (Ultralytics)

## Installation

1. **Clone the repository:**
    ```sh
    git clone https://github.com/MinaRafat22/ADAS-LKAS
    cd ADAS-LKAS
    ```

2. **Install the required libraries:**
    ```sh
    pip install opencv-python-headless numpy openni python-openni2 ultralytics
    ```

3. **Initialize OpenNI:**
    ```sh
    sudo apt-get install libopenni2-dev
    ```

4. **Download the YOLO model:**
    - Download the `best.pt` YOLO model and place it in the project directory.

## Parameters

- **Threshold:** The threshold for considering the drift that needs to be corrected (default: 4).
- **Maxstep:** The maximum difference in position between each frame for smoothing (default: 2).
- **Drift Correction:** A constant added to drift to compensate for camera placement (default: 0).

## Usage

1. **Connect the Kinect sensor** to your system.

2. **Run the script:**
    ```sh
    python final.py
    ```

3. **Adjust parameters** as needed directly in the script.

## Code Overview

- **Kinect Initialization:**
    ```python
    openni2.initialize()
    dev = openni2.Device.open_any()
    depth_stream = dev.create_depth_stream()
    depth_stream.start()
    color_stream = dev.create_color_stream()
    color_stream.start()
    ```

- **Overlay Image with Alpha Channel:**
    ```python
    def overlay_image_alpha(img, img_overlay, x, y, alpha_mask):
        ...
    ```

- **Determine Line Color:**
    ```python
    def determine_line_color(drift, threshold):
        ...
    ```

- **Find Center Lane:**
    ```python
    def find_center_lane(lanes, seg):
        ...
    ```

- **YOLO Model Initialization and Prediction:**
    ```python
    model = YOLO('best.pt')
    ```

- **Main Loop:**
    ```python
    while (1):
        ...
        results = model.predict(source=frame, show=False, conf=0.25, show_boxes=True)
        ...
    ```

## Output

- The system displays the color and depth frames from the Kinect sensor.
- Detected lane lines and vehicle position are shown on the video feed.
- Corrective messages are displayed if the vehicle is drifting out of the lane.

## Quitting

- Press `q` to quit the application.

## Notes

- Ensure that the Kinect sensor is properly connected and calibrated.
- Adjust the parameters as needed to fit your specific use case and environment.

