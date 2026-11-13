# LEGO EV3 Self-Balancing Robot

An experimental Python controller for a two-wheeled LEGO EV3 robot.
It combines gyro measurements and wheel encoders with a fixed-gain feedback
controller to perform a short balancing experiment.

## Hardware and runtime

The source uses **Python 3** and
[python-ev3dev2](https://github.com/ev3dev/ev3dev-lang-python) on an EV3 running
[ev3dev](https://www.ev3dev.org/). This is not a desktop Python simulation or a
Pybricks program.

| Connection | Component used by the source |
| --- | --- |
| Output A | Right wheel motor |
| Output D | Left wheel motor |
| Output B | Support/rack motor |
| Input 4 | Gyro sensor |

The physical build, polarity, and sensor orientation must match the controller's
assumptions. Its gains are specific to the original robot.

## Experiment flow

[main.py](main.py) calibrates gyro offset, estimates wheel/body state, applies
the feedback gains, clamps wheel duty cycle to `[-100, 100]`, and runs the
control loop for approximately ten seconds. It also raises and lowers the
support rack.

For an appropriately prepared EV3, the entry point is:

```sh
python3 main.py
```

**Hardware caution:** running or importing this file starts the experiment
because it calls `main()` at module level. It can move all three motors.
Review the wiring and control assumptions first, use a supported robot in a
clear test area, and keep the physical stop control accessible.
Successful balancing is not guaranteed for a different build.

## Source guide

The single-file implementation contains gyro calibration, sensing, numerical
integration and differentiation, feedback control, and rack movement helpers.
There is no CLI configuration, simulator, or packaged test harness.

The [ROBOTC counterpart](https://github.com/edoardorex/LegoEv3SegwayC) includes
build photographs and the original control-laboratory documents.

## Project provenance

This repository is a fork of
[edoardore/LegoEv3Segway](https://github.com/edoardore/LegoEv3Segway).
The original implementation and history are preserved.
