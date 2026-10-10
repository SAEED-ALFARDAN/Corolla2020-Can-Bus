# Automotive CAN Bus Reverse Engineering (Toyota Corolla 2020)

Passive CAN bus tap and signal-decoding project on my own 2020 Toyota Corolla.

**Status: work in progress.** A full write-up is coming. This page lists
only what I have captured so far, and marks what is still being re-verified.

## Scope and safety

- My own vehicle, tested while parked, on the body CAN bus.
- The tap is passive: it listens to bus traffic.
- Diagnostic (UDS) scanning was limited to identifying ECU addresses.
- Everything here requires physical access to the bus.
- Command sequences are intentionally not published.

## Setup

- Arduino Uno + MCP2515 CAN module
- Linux with SocketCAN, SavvyCAN for analysis
- Bus speed: 500 kbps

## Preliminary findings

| Function | CAN ID | Status |
|---|---|---|
| Window state | 0x638 | Verified in captured log |
| Door lock state | 0x4A5 | Verified in captured log |
| Gear position | 0x3BC | Decoded from notes, re-verification pending |
| Doors, handbrake, seatbelt | 0x620 | Decoded from notes, re-verification pending |
| Turn signals | 0x2D8 | Decoded from notes, re-verification pending |
| Wipers | 0x2F3 | Decoded from notes, re-verification pending |

Diagnostic scan: ABS (0x7B0), EPS (0x7A0), and A/C amplifier (0x7C0)
responded to diagnostic requests. The body ECU address is still unconfirmed.

## Method

1. Capture a baseline with the car idle.
2. Trigger one physical action (open a door, open trunk).
3. Compare captures, isolate the changing ID and bytes.
4. Repeat to confirm.

## Next

- Re-capture with raw logs for every signal above
- Confirm bus speed and service behavior of the diagnostic requests
- Publish the signal table, a DBC file, and decoding scripts
- Write up the security observations and possible mitigations

## Disclaimer

Educational research on my own vehicle. Do not test on a vehicle you don't own
or without permission.
