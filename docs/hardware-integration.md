# Hardware Integration

## Embedded Alert Path

The project connects the software recognition system to an Arduino Uno for a physical security response.

```text
Python Application
       │
       │ Serial Command
       ▼
  Arduino Uno
       │
       ▼
     Buzzer
```

## Why Use a Microcontroller?

The computer performs the computationally intensive computer-vision work. The Arduino is used as a simple embedded endpoint that converts an alert condition into a physical output.

This is a useful hardware/software co-design pattern:

- **Computer:** high-level processing and inference
- **Serial interface:** communication boundary
- **Microcontroller:** deterministic control
- **Buzzer:** physical indication

## Interface Considerations

A practical implementation needs a clearly defined serial command format and predictable behavior when an alert is received.

Important engineering considerations include:

- serial baud-rate agreement;
- valid command framing;
- handling unexpected input;
- avoiding repeated buzzer triggering from noisy events;
- defining a reset or timeout behavior;
- ensuring the physical output remains safe if communication stops.

## Future Hardware Extensions

The same interface concept could be extended to additional actuators or embedded controllers, such as:

- LED indicators;
- relay-controlled warning devices;
- display modules;
- network-connected microcontrollers;
- FPGA-based alert controllers.

The current academic implementation should be treated as a prototype rather than a production security controller.
