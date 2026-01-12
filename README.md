# Under_water_object_detection_system
🌊 IoT-Based Underwater Object Detection System
📌 Project Overview

This project presents an IoT-based real-time underwater object detection system capable of identifying marine debris, aquatic species, and submerged structures using a waterproof camera and Raspberry Pi–based edge processing.

The system captures live underwater video, processes it using computer vision and deep learning (YOLO + OpenCV), and transmits detection results wirelessly through IoT communication protocols for remote monitoring and analysis. The solution is cost-effective, scalable, and suitable for continuous underwater monitoring.

🎯 Objectives

Design and develop an IoT-based underwater object detection system

Implement machine learning and computer vision algorithms for object detection

Enable real-time wireless data transmission for remote monitoring

Analyze system performance under varying underwater conditions (lighting, turbidity, distance)

🌐 Domain

Internet of Things (IoT) & Machine Learning

❗ Problem Statement

Underwater environments are difficult to monitor due to:

Poor visibility and lighting

High equipment costs

Limited accessibility for continuous observation

Existing solutions rely on manual inspection, divers, or expensive robotic systems, making long-term monitoring impractical. This project addresses these issues by developing a low-cost, automated, and scalable underwater detection system.

⭐ Importance, Motivation & Scope⚙️ System Architecture (High Level)

Underwater Camera captures live visuals

Raspberry Pi 4 performs real-time inference using YOLO

ESP32 manages IoT communication and local feedback

LCD & Buzzer provide immediate alerts

Remote Dashboard enables wireless monitoring

🔄 Workflow

Dataset collection (underwater images/videos)

Annotation using Label Studio

Model training using YOLO lightweight variant

Deployment on Raspberry Pi

Real-time object detection

IoT-based data transmission

Monitoring and analysis

Early detection of marine pollution and debris

Support for marine research and environmental conservation

Scalable solution for underwater surveillance and exploration

Potential integration with autonomous underwater vehicles (AUVs) and advanced analytics🧰 Hardware Requirements

Raspberry Pi 4 (4GB)

ESP32 Microcontroller

Waterproof Camera

LCD Display

Monitor

Keyboard & Mouse

Power Supply / Battery

Supporting components (MicroSD, jumper wires)

💻 Software Requirements

Raspberry Pi OS (Linux)

Python (Raspberry Pi)

Arduino C (ESP32)

OpenCV

YOLO Model

NumPy, Pandas

MQTT / HTTP libraries

Label Studio (dataset annotation)

Arduino IDE, Thonny

📊 Implementation Details

YOLO model trained on annotated underwater dataset

Real-time inference executed on Raspberry Pi

ESP32 handles IoT communication and alert mechanisms

Detection results displayed on:

Monitor (bounding boxes, labels, confidence)

LCD screen (status alerts)

🧪 Results & Observations

Successful real-time underwater object detection

Improved accuracy after dataset fine-tuning

Low latency due to edge processing

Detection performance affected by:

Water clarity

Lighting conditions

Camera positioning

📈 Performance Analysis

Accuracy decreases as water turbidity increases

Clear water conditions give best results

Highlights need for larger datasets and sensor fusion

🌍 Applications

Marine research & coral monitoring

Environmental protection & pollution detection

Underwater surveillance and safety

Oceanographic studies

Aquaculture & fisheries

Underwater exploration & archaeology

⏳ Use Cases
Short-Term

Controlled tank testing

Academic and student research

Long-Term

Large-scale ocean and river deployment

Integration with underwater drones

Cloud-based analytics and monitoring

🔮 Future Enhancements

Improve accuracy using larger datasets

Handle low-light and high-turbidity conditions better

Integrate sonar and underwater drones

Add object tracking and cloud analytics

Enable human/diver detection for safety and rescue operations

👩‍💻 Team Members

Pooja Mahesh Gangnaik (1BI22EC107)

Prakruthi G (1BI22EC110)

Nidhi V (1BI22EC096)

Pooja B M (1BI22EC106)

Guide:
Swathi – Assistant Professor, Dept. of ECE, BIT Bangalore

🏁 Conclusion

The project successfully demonstrates that low-cost edge devices combined with AI and IoT can perform reliable real-time underwater object detection. It provides strong practical exposure in deep learning, embedded systems, sensing, and IoT communication, and shows high potential for real-world deployment.

📚 References

IEEE – Underwater Monitoring Systems

Automatic Fish Detection using ML

IoT-Based Marine Litter Detection

Improved YOLO-based Underwater Detection

AIoT-based Underwater Trash Management



