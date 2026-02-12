# Modbus TCP – Unauthorized Write Attack Simulation

## Executive Summary

This exercise simulates unauthorized Modbus TCP write activity against an industrial control register and demonstrates detection, packet analysis, and SOC-style incident documentation.

The objective is to replicate how an attacker could manipulate process variables and how a SOC analyst would detect and document the activity.

---

## Environment

- Protocol: Modbus TCP
- Default Port: 502
- Tool Used: mbpoll (for simulation)
- Packet Analysis: Wireshark
- Lab Context: OT/ICS environment

---

## Phase 1 – Establish Baseline (Normal Read)

Perform a legitimate Modbus read:

- Function Code: 03 (Read Holding Register)
- Capture traffic in Wireshark
- Record baseline register value

### Wireshark Filter:
tcp.port == 502

Document:
- Source IP
- Destination IP
- Unit ID
- Function Code
- Register Address
- Baseline Value

---

## Phase 2 – Unauthorized Write Simulation

Simulate an unauthorized write:

- Function Code: 06 (Write Single Register)

Observe:
- Register value change
- Write request packet
- Write response packet
- Transaction ID
- Payload data

### Write Detection Filter:

modbus.func_code == 6
---

## Evidence Collected

- PCAP capture of write request
- PCAP capture of write response
- Register value before and after modification
- Command execution logs

---

## Detection Opportunities (SOC Perspective)

A Modbus write (FC06 or FC16) from an unexpected source may indicate:

- Process manipulation attempt
- Malicious insider activity
- Compromised engineering workstation
- Lateral movement into OT network segment

---

## MITRE ATT&CK (ICS) Mapping

| Technique | Description |
|-----------|-------------|
| T0855 | Unauthorized Command Message |
| T0831 | Manipulation of Control |
| T0842 | Network Sniffing |
| T0807 | Command-Line Interface |

---

## Defensive Recommendations

- Monitor Modbus write function codes (06, 16)
- Restrict write operations via network segmentation
- Establish baseline register behavior
- Alert on abnormal write frequency



