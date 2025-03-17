# FloodGuard: Real-time Flood Detection with WhatsApp Alerting System

## Overview
FloodGuard is an intelligent monitoring system that uses computer vision to detect flooding events in real-time through video streams. When flooding is detected, the system automatically sends WhatsApp alerts to emergency responders, authorities, or community members, enabling rapid response to minimize damage and protect lives.

## Features
- **Real-time Flood Detection**: Processes video streams using a trained YOLOv8 model specifically tuned for flood detection
- **WhatsApp Alert System**: Automatically sends notifications with location information when flooding is detected
- **Web-based Dashboard**: Provides a live monitoring interface with real-time status updates
- **REST API**: Offers endpoints for system status, video feeds, and event monitoring
- **Video Processing**: Works with both live camera feeds and pre-recorded footage for testing

## Technical Architecture
The system consists of two main components:
1. **Detection Engine**: YOLO-based CV model processes video frames to identify flood events
2. **Notification System**: REST API integration with WhatsApp to deliver alerts

## Requirements
- Python 3.8+
- OpenCV
- Flask
- Ultralytics YOLO
- Requests
- Pre-trained flood detection model (`best.pt`)
- WhatsApp notification endpoint (e.g., using Twilio API or custom webhook)

## Installation

1. Clone the repository
```bash
git clone https://github.com/yourusername/floodguard.git
cd floodguard
```

2. Install dependencies
```bash
pip install -r requirements.txt
```

3. Download the pre-trained model (`best.pt`) and place it in the project root directory.

4. Configure the environment variables
```bash
# Create .env file for configuration
touch .env
```

## Configuration
Edit the `.env` file with your API keys and endpoints:

```
# WhatsApp notification endpoint
NOTIFICATION_ENDPOINT=https://your-whatsapp-notification-endpoint.com/flood-alert

# Google Maps API key (for location services)
GOOGLE_MAPS_API_KEY=your_google_maps_api_key

# Flask secret key
FLASK_SECRET_KEY=your_flask_secret_key
```

Additionally, you can modify settings in flood_detection.py:
- Change the video source (`video_path`)
- Adjust detection sensitivity by modifying the confidence threshold (`conf=0.25`)
- Customize the alert message and location information

## Usage

1. Start the Flask server
```bash
python flood_detection.py
```

2. Access the web interface
   - Open your browser and navigate to `http://localhost:5000`
   - View the live video stream with flood detection overlay
   - Monitor alert status in real-time

3. API Endpoints
   - `/video_feed`: Live video stream with detection overlay
   - `/flood_status`: Current flood detection status in JSON format
   - `/flood_events`: Server-sent events for real-time notifications

## WhatsApp Integration

The system uses a webhook endpoint to trigger WhatsApp notifications. When flooding is detected:

1. The system sends a GET request to the configured endpoint
2. The request includes the location where flooding was detected
3. The WhatsApp message includes:
   - Alert notification
   - Confidence level of detection
   - Time of detection
   - Location information

To set up your own WhatsApp notification service, you can use:
- Twilio API
- WhatsApp Business API
- Custom webhook that forwards messages to WhatsApp

## Environmental Data Integration

The system can also be integrated with the EnvGuard environmental monitoring component to provide additional data points about air quality and other environmental factors in flood-affected areas.

## Screenshots
![Flood Detection Dashboard](https://example.com/screenshots/dashboard.png)
*(Add your actual screenshots here)*

## Future Enhancements
- Multi-camera support for wider coverage
- Integration with weather forecasting APIs
- Mobile application for field responders
- Advanced analytics for flood prediction
- Community alert subscription system
- Integration with municipal emergency systems

## Important Notes
- This system is designed as an assistive tool and should not replace official emergency systems
- Always verify flood detections through multiple sources before taking action
- Configure alert thresholds carefully to avoid false alarms
- Test the system regularly to ensure proper operation

## License
MIT License

## Acknowledgements
- YOLOv8 for object detection capabilities
- Google Maps API for location services
- Flask community for the web framework
