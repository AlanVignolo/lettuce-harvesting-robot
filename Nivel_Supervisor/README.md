# Supervisor level

Python 3 application that runs on the Raspberry Pi. Owns the state machine, the camera, the vision pipeline, and the UART link down to the regulatory level.

## Layout

- `main.py` — entry point; interactive menu (simple start, full start, full start with calibration, interactive harvest, simple homing).
- `controller/robot_state_machine.py` — `RobotStateMachine`: the top-level state machine that sequences homing, scanning, classification, and harvest.
- `core/robot_controller.py` — `RobotController`: mid-level API over the command layer (movement, arm, status).
- `core/camera_manager.py` — camera capture (threaded, queued frames).
- `hardware/uart_manager.py` — UART transport to the regulatory level (framing, timeouts, retries).
- `hardware/command_manager.py` — builds and sends `<CMD:...>` frames, matches responses to requests.
- `robot/arm_controller.py`, `robot/trajectories.py`, `robot/arm_states.py` — arm sequencing (pick, transport, deposit) and predefined trajectories.
- `workflows/workflow_orchestrator.py` — the concrete workflows exposed in the menu (`inicio_simple`, `inicio_completo`, `inicio_completo_hard`, `cosecha_interactiva`, `homing_simple`).
- `config/robot_config.py` — hardware and calibration constants.

## Running

```
pip install -r requirements.txt
python main.py
```

Requires a UART connection to the regulatory-level microcontroller and a USB camera. See the [vision modules](../Nivel_Supervisor_IA/) for the detectors this level calls into, and the [main README](../README.md) for the overall architecture.
