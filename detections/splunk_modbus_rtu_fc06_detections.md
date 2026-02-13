# Splunk Detection Logic – Modbus RTU (FC06)

These detections assume FC06 write events are logged as key=value lines, e.g.:

modbus_rtu_write fc=6 slave=1 reg=5 value=9600 port="/dev/ttyUSB0" status=success

---

## 1) Detect ANY Modbus RTU Write (FC06)

```spl
index=main modbus_rtu_write fc=6

Commit.

---

# ✅ Step 3 — Add one “alert recipe” (so a recruiter can copy/paste)

In your README, add:

```markdown
## Detection Example (Splunk)

To detect unauthorized Modbus RTU writes (FC06):

```spl
index=main modbus_rtu_write fc=6

Commit.

---

# ✅ Step 4 — Verify in Splunk (fast)

Run your `rtu_fc06_attack_proof.py` again.

Then in Splunk search:

```spl
index=main modbus_rtu_write fc=6
