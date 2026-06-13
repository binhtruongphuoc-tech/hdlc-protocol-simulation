# hdlc-protocol-simulation
Theoretical analysis and practical simulation of Layer 2 HDLC/cHDLC encapsulation and data link mechanisms

# HDLC Protocol Analysis & WAN Simulation 

A networking project focused on the deep theoretical analysis and practical simulation of the High-Level Data Link Control (HDLC) protocol. Utilizing Cisco Packet Tracer, this project demonstrates how Layer 3 IP packets are encapsulated into Layer 2 HDLC frames for transmission over Wide Area Network (WAN) serial links.

---

## Project Overview

HDLC is a bit-oriented synchronous data link layer protocol developed by ISO. This project bridges the gap between networking theory and practical configuration by analyzing the exact frame structure and simulating a point-to-point serial connection between Cisco routers.

### Core Simulation Features
* **Topology:** A point-to-point WAN topology connecting two routing nodes via Serial DCE/DTE interfaces.
* **Encapsulation:** Configured the `encapsulation hdlc` command on serial interfaces to enforce Cisco's proprietary cHDLC framing.
* **Verification:** Validated the Layer 2 data link state using `show interfaces serial` and confirmed end-to-end Layer 3 connectivity with 100% successful ICMP Echo Requests (`ping`).

---

## Protocol Architecture Analysis

A major focus of this project is understanding how data is structured on the wire. The implementation utilizes **Cisco HDLC (cHDLC)**, which introduces a "Protocol" field to the standard ISO HDLC frame to support multi-protocol environments.

**HDLC Frame Structure Analyzed:**
1. **Flag (8 bits):** `01111110` - Marks the beginning and end of the frame for synchronization.
2. **Address (8 bits):** Identifies the secondary station (destination).
3. **Control (8/16 bits):** Defines the frame type (Information, Supervisory, or Unnumbered) and manages flow/error control.
4. **Protocol (16 bits - Cisco specific):** Specifies the network layer protocol (e.g., IPv4) encapsulated within the frame.
5. **Information (Variable):** The actual payload (Layer 3 packet).
6. **FCS (16/32 bits):** Frame Check Sequence for cyclic redundancy check (CRC) error detection.

---

## 📸 Simulation Gallery


| Network Topology | HDLC Interface Verification | End-to-End Ping Test |
| :---: | :---: | :---: |
| ![Topology](images/topology.png) | ![Show Interface](images/show_interface.png) | ![Ping Test](images/ping_test.png) |

---
##  Advanced cHDLC Frame Analysis

In a synchronous WAN environment, Layer 2 encapsulation is critical for data integrity. Unlike standard ISO HDLC, this project utilizes **Cisco HDLC (cHDLC)**, which adds a "Protocol" field to support multi-protocol environments.

![cHDLC Frame vs Standard HDLC](images/chdlc_frame.png)

**Frame Structure Breakdown:**
* **Flag (`0x7E`):** Marks the frame's start/end. Uses bit-stuffing to prevent data collision.
* **Address (`0x0F` / `0x8F`):** Identifies the destination in a Point-to-Point link.
* **Control (`0x00`):** Manages flow and sequence numbers (I-frame).
* **Protocol (`0x0800` for IPv4):** *Cisco-specific addition.* Allows the router to identify the encapsulated Layer 3 protocol.
* **FCS (16/32-bit):** Frame Check Sequence using CRC to detect transmission errors.

---


##  Tools & Concepts
* **Environment:** Cisco Packet Tracer
* **Key Concepts:** Wide Area Networks (WAN), Data Link Layer (OSI Layer 2), HDLC/cHDLC Encapsulation, Serial Communication (DCE/DTE), Synchronous Transmission.
