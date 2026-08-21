# System Architecture

## High-Level Design

The project separates the system into two cooperating domains:

1. **Host-side intelligence** — camera capture, face detection, face encoding, recognition, tracking, and decision logic.
2. **Embedded alert layer** — serial command reception on Arduino Uno and physical buzzer activation.

```text
                    HOST COMPUTER
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  Camera → Detection → Encoding → Matching → Tracking   │
│                                      │                   │
│                                      ▼                   │
│                              Recognition Decision        │
│                                │             │           │
│                              Known         Unknown       │
│                                │             │           │
│                                ▼             ▼           │
│                             Display       Alert Logic    │
│                                              │           │
└──────────────────────────────────────────────┼───────────┘
                                               │ Serial
                                               ▼
                                      ┌────────────────┐
                                      │   Arduino Uno  │
                                      └───────┬────────┘
                                              │
                                              ▼
                                           Buzzer
```

## Major Components

### Camera

Provides the live image stream used as the input to the vision pipeline.

### Face detector

The implementation uses HOG-based face detection to locate faces in frames.

### Face encoder

Detected faces are converted into numerical 128-dimensional representations. These embeddings provide a compact representation that can be compared against registered identities.

### Recognition layer

The recognition stage compares a live face representation with stored known-face representations and determines whether the observed face matches a registered identity.

### Tracking and temporal decision layer

Tracking associates observations across frames. Recognition history can then be used to stabilize decisions instead of treating every frame as an independent event.

### Alert layer

Unknown-person events can be forwarded to the embedded subsystem through serial communication.

### Arduino alert controller

The Arduino receives the alert condition and drives the connected buzzer, providing a physical indication of a security event.

## Engineering Boundary

The division of work is deliberate: computationally expensive vision operations remain on the host computer, while the microcontroller performs a simple deterministic physical-response task.

This architecture also makes the embedded interface easy to replace later with another controller, actuator, or communication mechanism.
