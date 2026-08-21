# Face Recognition Concepts

## Detection vs Recognition

These are separate stages:

- **Detection:** where is a face in the current image?
- **Recognition:** whose face is it, if it belongs to a registered identity?

Keeping these stages conceptually separate makes the pipeline easier to optimize and debug.

## HOG-Based Detection

The project uses a Histogram of Oriented Gradients (HOG)-based approach for face detection. HOG represents local image structure using gradient-orientation information and can provide a practical CPU-oriented detection method for an academic real-time prototype.

## 128-D Face Encoding

A detected face is represented as a 128-dimensional numerical encoding. Recognition is performed by comparing these encodings rather than directly comparing complete images.

The quality of the final decision depends on factors such as image quality, pose, illumination, face size, and the matching threshold.

## Registration

The project includes a registration workflow for creating the known-face reference set. A registered identity is associated with one or more face representations that can later be used during recognition.

## Recognition Stability

Real-time video produces many observations of the same person. A single observation can be noisy, so the system also uses tracking and recognition history to improve temporal stability.

This is an important practical distinction between a one-image demonstration and a real-time recognition pipeline.

## Security Limitations

Face recognition is biometric processing and therefore introduces important security and privacy considerations. A stronger deployment would need protections against presentation attacks, secure storage of biometric representations, access control, auditing, and careful handling of false matches.
