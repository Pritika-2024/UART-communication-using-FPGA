# UART Communication using FPGA

![FPGA](https://img.shields.io/badge/Platform-Spartan6%20FPGA-blue?style=for-the-badge)
![Language](https://img.shields.io/badge/Language-Verilog-orange?style=for-the-badge)
![Software](https://img.shields.io/badge/Software-Xilinx%20ISE%2014.7-red?style=for-the-badge)

> FPGA-based UART (Universal Asynchronous Receiver-Transmitter) communication system implemented using Verilog HDL on the Mimas V2 Spartan-6 FPGA board.

---

# Table of Contents

- Overview
- How It Works
- Architecture
- Simulation
- Hardware Implementation
- Components
- Results
- Future Scope

---

# Overview

This project implements a complete UART communication system directly in FPGA hardware using Verilog HDL. The system establishes serial communication between a PC and the Spartan-6 MimasV2 FPGA board.

The design includes:

- UART Transmitter
- UART Receiver
- Baud Rate Generator
- Parity Detection
- Seven Segment Display Output

The project was designed and synthesized using **Xilinx ISE 14.7** and tested on the **Mimas V2 Spartan-6 FPGA Board**.

---

#  How It Works

The UART transmitter converts parallel data into serial format and sends it through the TX line. The UART receiver detects incoming serial data on the RX line, reconstructs the original byte, and displays the received data on seven-segment displays. FPGA Sprtan6 MimasV2 is designed for **19200 bps rate**.

The communication frame consists of:

- 1 Start Bit
- 8 Data Bits
- 1 Stop Bit

Data is transmitted in **LSB-first** format.

<p align="center">
<b> UART Block Diagram </b><br>
<img src="./docs/block_diagram.png" width="650">
</p>

---

# Architecture

The UART system consists of:

- Baud Rate Generator
- UART Transmitter
- UART Receiver
- Top-Level Module
- Seven Segment Display Driver

<p align="center">
<b> UART Architecture </b><br>
<img src="./docs/uart_architecture.png" width="700">
</p>

---

# Receiver Module

The UART receiver continuously monitors the RX line and reconstructs incoming serial data.

Receiver FSM states:

| State | Function |
|---|---|
| IDLE | Wait for START bit |
| START | Validate START bit |
| DATA | Receive data bits |
| STOP | Validate STOP bit |

<p align="center">
<b> Receiver FSM </b><br>
<img src="./docs/rx_fsm.png" width="500">
</p>

---

#  Transmitter Module

The transmitter serializes 8-bit parallel data into UART frames.

Transmitter FSM states:

| State | Function |
|---|---|
| IDLE | Wait for transmission |
| START | Send START bit |
| DATA | Send serial data |
| STOP | Send STOP bit |

<p align="center">
<b> Transmitter FSM </b><br>
<img src="./docs/tx_fsm.png" width="500">
</p>

---

#  Simulation

Simulation was performed using **ISim Simulator** in Xilinx ISE 14.7.

The simulation verified:

- Correct UART frame generation
- Proper baud synchronization
- Correct serialization/deserialization
- Successful data transmission and reception

<p align="center">
<b> Simulation Waveform </b><br>
<img src="./docs/simulation_waveform.png" width="700">
</p>

---

#  Hardware Implementation

The UART system was programmed onto the Mimas V2 Spartan-6 FPGA board and tested using PuTTY serial terminal communication. For error detection parity bit (first segment) along with charecter(second segment) is displayed on on-board seven segment.

<p align="center">
<b> Hardware Setup </b><br>
<img src="./docs/hardware_setup.png" width="500">
<img src="./docs/putty.png" width="500">
</p>

---

#  Components

| # | Component |
|---|---|
| 1 | Mimas V2 Spartan-6 FPGA Board |
| 2 | Seven Segment Display |
| 3 | Xilinx ISE 14.7 |
| 4 | ISim Simulator |
| 5 | PuTTY Terminal |

---

#  Results

The UART system successfully demonstrated:

- Reliable UART communication
- Correct serial transmission and reception
- Stable operation at 19200 baud rates
- Correct parity generation
- Successful loopback testing

| Test Case | Result |
|---|---|
| UART Transmission | Successful |
| UART Reception | Successful |
| Loopback Communication | Successful |
| Baud Synchronization | Successful |
| Parity Detection | Successful |

---

#  Future Scope

- FIFO Buffer Integration
- Multi-channel UART
- Higher Baud Rates
- UART to SPI/I2C Bridge
- AXI Bus Integration

---


# 📖 References

1. Spartan-6 FPGA Datasheet  
2. Xilinx ISE 14.7 Documentation
3. Nandland Fpga UART website
