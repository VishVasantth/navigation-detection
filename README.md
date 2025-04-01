# OSM Navigation with Real-time Object Detection

A navigation system using OpenStreetMap (OSM) that includes real-time object detection for obstacle avoidance.

## Overview

This project integrates:
1. OpenStreetMap-based navigation
2. Real-time object detection using YOLOv8
3. Dynamic path planning with obstacle avoidance

The system is designed for robots to follow a path while detecting and avoiding obstacles in real time.

## Features

- Interactive map with multiple routing options
- Path planning using GraphHopper API
- Real-time object detection using YOLOv8
- Automatic obstacle placement and path rerouting
- Simulation for testing path planning

## Requirements

### Frontend
- Node.js 14+
- npm or yarn

### Backend
- Python 3.8+
- OpenCV
- Ultralytics YOLOv8
- Flask

## Project Structure

```
/
├── frontend/         # React frontend application
├── backend/          # Flask API and object detection
│   ├── detection/    # YOLOv8 integration
│   └── app.py        # Backend server
├── yolov8n.pt        # YOLOv8 model weights
└── run_all.py        # Script to run all services
```

## Installation

1. Clone the repository:
   ```
   git clone <repository-url>
   cd <repository-folder>
   ```

2. Install frontend dependencies:
   ```
   cd frontend
   npm install
   cd ..
   ```

3. Install backend dependencies:
   ```
   pip install -r backend/requirements.txt
   ```

4. Ensure you have YOLOv8 weights file (`yolov8n.pt`) in the project root.

## Running the Application

### Option 1: Run everything at once

```
python run_all.py
```

This will start both the frontend and backend servers and display their outputs.

### Option 2: Run servers separately

1. Start the backend server:
   ```
   cd backend
   python run.py
   ```

2. Start the frontend server:
   ```
   cd frontend
   npm start
   ```

3. Open your browser to `http://localhost:3000`

## Usage

1. **Select Start and Destination**: Choose locations from the dropdown or enter coordinates
2. **Find Path**: Click "Find Path" to plan a route
3. **Simulate Movement**: Click "Simulate Movement" to test navigation
4. **Object Detection**: Click "Start Detection" to activate the camera and detect objects
5. **Manual Obstacles**: Place obstacles manually by clicking "Place Obstacle" and then clicking on the map

## Object Detection to Obstacle Workflow

When "Start Detection" is activated:
1. Camera feed starts and is processed by YOLOv8
2. Detected objects that match obstacle classes are identified
3. Objects are mapped to GPS coordinates and placed on the map
4. If an obstacle is in the path, the route is automatically recalculated

## API Endpoints

### Backend API (port 5001)
- `POST /start`: Start object detection
- `POST /stop`: Stop object detection
- `GET /frame`: Get current video frame
- `GET /objects`: Get detected objects

## Configuration

### Frontend
- `REACT_APP_BACKEND_URL`: Main backend URL (default: http://localhost:5000)
- `REACT_APP_DETECTION_URL`: Detection service URL (default: http://localhost:5001)
- `REACT_APP_GRAPHHOPPER_API_KEY`: GraphHopper API key for routing

### Backend
- `PORT`: Backend server port (default: 5001)

## Troubleshooting

- If the camera doesn't start, make sure your webcam is properly connected and accessible
- For better performance with object detection, a system with GPU is recommended
- If paths don't appear, check your GraphHopper API key configuration
- The coordinate mapping for detected objects is approximate and may need calibration

## License

This project is licensed under the MIT License - see the LICENSE file for details. 