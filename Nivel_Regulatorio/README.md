# Regulatory level (firmware)

Atmel Studio / AVR C project. Runs on the microcontroller and handles everything that needs hard real-time response: stepper motion, servo/gripper actuation, limit switches, and the UART link to the supervisor.

## Layout

- `main.c` — init + main loop (`stepper_update_profiles`, `servo_update`, `gripper_update` polled every cycle).
- `drivers/stepper_driver.*` — stepper step generation and axis state.
- `moves/motion_profile.c`, `drivers/motion_profile_simple.*` — trapezoidal velocity profile generation (acceleration/cruise/deceleration) for coordinated multi-axis moves.
- `drivers/encoder_driver.*` — step/position tracking.
- `drivers/servo_driver.*`, `drivers/gripper_driver.*` — arm servos and gripper actuation.
- `drivers/uart_driver.*` — UART transport (256-byte circular buffer).
- `command/command_parser.*` — parses `<CMD:param1,param2>` frames and dispatches to drivers.
- `limits/limit_switch.*` — homing and travel-limit switches, wired to stop the corresponding axis immediately on trigger.
- `config/system_config.h`, `config/command_protocol.h` — pin mapping, timing constants, and the command set definition.

## Protocol

ASCII, newline-terminated: `<COMMAND:param1,param2>\n`. Successful commands return `RESPONSE...`; failures return `ERROR...`. The firmware also pushes unsolicited events (`<STEPPER_MOVE_COMPLETED:x,y>`, `<LIMIT_TRIGGERED:type>`, `<GRIPPER_OPENED>`, `<GRIPPER_CLOSED>`, `<STEPPER_EMERGENCY_STOP>`) so the supervisor doesn't have to poll. Full command table in the main [README](../README.md#architecture) and in `Informe/03_Desarrollo/3.3_nivel_regulatorio/estructura_comandos.tex`.

## Building

Open `Nivel_Regulatorio.atsln` in Atmel Studio (or build with `avr-gcc` using the same source layout) and flash to the target AVR microcontroller.
