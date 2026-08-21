# Software Pipeline

## Processing Flow

```text
Frame Capture
     ↓
Face Detection
     ↓
Face Encoding
     ↓
Known-Face Comparison
     ↓
Tracking / Recognition History
     ↓
Stable Decision
     ├── Known   → Identity Display
     └── Unknown → Security Event
                         ↓
                    Alert Interface
```

## Real-Time Considerations

The application has to balance recognition quality with responsiveness. Camera capture, image processing, and user-interface updates should not unnecessarily block one another.

The project therefore uses a modular processing approach in which recognition work can be handled independently from the main application flow.

## Face Representation

A detected face is converted into a **128-dimensional encoding**. Rather than comparing raw images pixel-by-pixel, the system compares these numerical representations.

This allows a live observation to be matched against a collection of registered face encodings.

## Temporal Decision Making

Recognition can fluctuate between frames because of pose, lighting, motion, partial occlusion, or detection noise. Tracking and recognition history provide additional temporal information.

A practical consequence is that the application can make a decision using a sequence of observations rather than trusting a single frame.

## Unknown Event Flow

When a face does not correspond to a registered identity, the event can be passed to the alert subsystem. The design supports capturing an image of an unknown event and sending an alert command toward the Arduino layer.

## Software Organization

The original project was separated into modules for application control, registration, face utilities, recognition processing, tracking, alerts, and configuration. This separation makes the project easier to reason about and allows individual parts of the pipeline to evolve independently.

## Important Caveat

This document describes the architecture and engineering concepts of the academic project. The original team's source implementation is intentionally excluded from this public portfolio repository.
