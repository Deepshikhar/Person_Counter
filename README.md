# Person Counter with YOLOv11

A real-time person counting system that uses YOLOv11 object detection and tracking to monitor people entering and exiting defined areas in video streams.

## Features

- **Real-time Detection**: Utilizes YOLOv11 models for fast and accurate person detection
- **Object Tracking**: Implements ByteTrack algorithm for consistent object tracking across frames
- **Dual Counting Zones**: Supports separate entry and exit counting with customizable polygonal areas
- **Multiple Model Support**: Compatible with various YOLOv11 model sizes (n, s, m, l)
- **Flexible Input Sources**: Works with video files, webcam feeds, or other video sources
- **Performance Metrics**: Displays real-time FPS for performance monitoring
- **Video Export**: Option to save processed videos with annotations and counters

## Prerequisites

Before running this project, ensure you have the following installed:

- Python 3.8 or higher
- PyTorch (>=1.7.0)
- OpenCV (>=4.5.0)
- Ultralytics YOLO package

## Installation

1. Clone or download this project to your local machine

2. Install required packages:

```bash
pip install ultralytics opencv-python
```

3. For optimal performance, install PyTorch with CUDA support (if you have an NVIDIA GPU):

```bash
# For CUDA 11.3
pip install torch==1.12.0+cu113 torchvision==0.13.0+cu113 -f https://download.pytorch.org/whl/torch_stable.html
```

## Model Files

This project supports various YOLOv11 model sizes. The models will be automatically downloaded on first use:

- **YOLOv11n** (Nano): Fastest, lowest accuracy - ideal for real-time applications
- **YOLOv11s** (Small): Balanced speed and accuracy
- **YOLOv11m** (Medium): Good balance for most applications
- **YOLOv11l** (Large): Highest accuracy, slower processing

## Usage

Run the person counter with the following command structure:

```bash
python person-counter.py --model [MODEL_PATH] --video [VIDEO_SOURCE] --conf [CONFIDENCE] --save
```

### Parameters

- `--model`: Specify which YOLOv11 model to use (default: `yolo11l.pt`)
- `--video`: Path to video file or webcam index (0 for default webcam)
- `--conf`: Confidence threshold for detection (0.0-1.0, default: 0.25)
- `--save`: Include this flag to save the processed video

### Examples

1. **Webcam with default settings**:
```bash
python person-counter.py --video 0
```

2. **Video file with YOLOv11n model**:
```bash
python person-counter.py --model models/yolo11n.pt --video inference/videos/hotel.mp4
```

3. **Higher confidence threshold with save option**:
```bash
python person-counter.py --model models/yolo11m.pt --video inference/videos/shopping_mall.mp4 --conf 0.5 --save
```

4. **Custom video with large model**:
```bash
python person-counter.py --model models/yolo11l.pt --video inference/videos/office.mp4 --conf 0.3
```

## Customization

### Adjusting Counting Areas

The counting areas are defined as polygons in the code. To modify them, update the coordinates in the main script:

```python
# Entry Count Area (Polygon defined by 4 points for counting entries)
entry_area = {
    'point1': (515, 434),  # Top-left corner
    'point2': (668, 376),  # Top-right corner
    'point3': (713, 435),  # Bottom-right corner
    'point4': (561, 497),  # Bottom-left corner
}

# Exit Count Area (Polygon defined by 4 points for counting exits)
exit_area = {
    'point1': (67, 570),   # Top-left corner
    'point2': (318, 452),  # Top-right corner
    'point3': (363, 502),  # Bottom-right corner
    'point4': (109, 632),  # Bottom-left corner
}
```

### Performance Tuning

- For **better performance** (higher FPS): Use smaller models (`yolo11n.pt`, `yolo11s.pt`) and lower confidence thresholds
- For **higher accuracy**: Use larger models (`yolo11m.pt`, `yolo11l.pt`) and increase confidence threshold

## Output

The system provides:
- Real-time video display with bounding boxes and tracking trails
- IN/OUT counters showing people entering and exiting
- FPS counter for performance monitoring
- Optional video export with all annotations

Saved videos are stored in the `result/` directory with the same name as the input file.

## Result video (embedded)

<video src="[result/hotel.mp4](https://github.com/Deepshikhar/Person_Counter/blob/main/result/hotel.mp4)" controls style="max-width: 100%;"></video>

## Troubleshooting

### Common Issues

1. **Model not found**: Models are automatically downloaded on first run. Ensure you have internet connection.

2. **Low FPS**: 
   - Try using a smaller model (`yolo11n.pt`)
   - Reduce video resolution if processing webcam
   - Lower the confidence threshold

3. **Webcam not working**:
   - Verify webcam index (try 0, 1, or 2)
   - Check if webcam is being used by another application

4. **CUDA out of memory**:
   - Use a smaller model
   - Reduce input video resolution
   - Close other GPU-intensive applications

## Resources

- [YOLO Masterclass Course](https://www.udemy.com/course/yolo-masterclass-deep-learning-computer-vision-course/)
- [Ultralytics YOLOv11 Documentation](https://docs.ultralytics.com/)
- [PyTorch Official Website](https://pytorch.org/)
- [OpenCV Documentation](https://docs.opencv.org/)

## Project Structure

```
person-counter/
├── person-counter.py     # Main application script
├── result/              # Output directory for saved 
├── models/
    └── yolo11l.pt
    └── yolo11m.pt
    └── yolo11n.pt
    └── yolo11s.pt
├── inference/           # Input videos directory
│   └── videos/
│       └── hotel.mp4    # Example video file
└── README.md           # This file
```

## Future Enhancements

Potential improvements for this project:
- Support for multiple counting zones
- Directional counting (left-to-right, right-to-left)
- Crowd density estimation
- Integration with databases for long-term analytics
- Web interface for remote monitoring

## License

This project is intended for educational purposes as part of the YOLO Masterclass course. Please respect the licensing terms of the Ultralytics YOLO models and any third-party video content used for testing.

---

*Note: This project demonstrates practical implementation of computer vision techniques for real-world applications. Adjust parameters and counting areas according to your specific use case.*
