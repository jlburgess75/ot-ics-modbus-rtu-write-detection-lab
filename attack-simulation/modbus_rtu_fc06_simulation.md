# Modbus RTU – Unauthorized Write Simulation (FC06)

## Objective
Simulate unauthorized Modbus RTU write activity against register `reg=5`.

---

## Phase 1 – Baseline Read (FC03)
Read register to establish known value.

Expected:
- minimalmodbus debug output
- Splunk telemetry event

---

## Phase 2 – Unauthorized Write (FC06)
Execute write to register.

Expected:
- FC06 transaction visible
- Splunk event:
  modbus_rtu_write fc=6 reg=5 status=success

---

## Phase 3 – Verification Read
Confirm register value changed.

---

## Detection Opportunity
Monitor for:
- fc=6 writes
- sensitive register writes
- burst write frequency
- after-hours activity
