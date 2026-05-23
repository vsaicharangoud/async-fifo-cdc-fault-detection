# Self-Diagnosing Asynchronous FIFO with Runtime CDC Fault Detection

A parameterized asynchronous FIFO designed in **Verilog HDL** for reliable Clock Domain Crossing (CDC) communication between independent clock domains.  
The design integrates a dedicated **runtime diagnostic unit** capable of detecting CDC-related faults such as Gray-code violations, overflow, underflow, and pointer stall conditions without affecting normal FIFO operation.

---

# Project Overview

Modern System-on-Chip (SoC) architectures frequently operate with multiple independent clock domains.  
Reliable data transfer between these domains is a major challenge due to:

- Metastability
- Synchronization failures
- Data corruption
- Pointer inconsistencies

This project implements a **CDC-safe asynchronous FIFO** using:

- Gray-coded pointer synchronization
- Multi-stage synchronizers
- Runtime fault-monitoring architecture

Unlike conventional asynchronous FIFOs, this design actively monitors internal FIFO behavior and provides runtime diagnostic visibility.

---

# Key Features

- Dual-clock asynchronous FIFO
- Independent write and read clock domains
- Gray-coded pointer synchronization
- Multi-stage CDC synchronizers
- FIFO full and empty detection
- Overflow and underflow monitoring
- Sticky fault indicators
- Runtime CDC fault detection
- Pointer stall detection
- Parameterized RTL architecture
- FPGA/ASIC synthesizable design
- Modular Verilog implementation

---

# Architecture

The architecture consists of the following major blocks:

- FIFO Memory
- Write Pointer Handler
- Read Pointer Handler
- Pointer Synchronizers
- Self-Diagnosis Unit

The diagnostic unit continuously monitors FIFO activity and reports abnormal conditions during runtime.

---

# Runtime Diagnostic Features

The integrated Self-Diagnosis Unit detects:

| Fault Type | Description |
|---|---|
| Gray Code Violation | Detects invalid multi-bit Gray-code transitions |
| Overflow Detection | Detects writes attempted when FIFO is full |
| Underflow Detection | Detects reads attempted when FIFO is empty |
| Pointer Stall Detection | Detects stuck pointers during active operations |
| Sticky Fault Flags | Retains fault status for debugging visibility |

---

# CDC Handling Technique

To ensure reliable asynchronous communication:

- Binary pointers are converted into Gray code
- Only one bit changes between consecutive Gray-code values
- Multi-stage synchronizers safely transfer pointers across clock domains
- Registered full/empty logic prevents glitches

This significantly reduces metastability risks during pointer synchronization.

---

# Directory Structure

```text
async-fifo-cdc-fault-detection/
│
├── rtl/
│   ├── async_fifo_top.v
│   ├── wr_domain.v
│   ├── rd_domain.v
│   ├── sync_ptr.v
│   ├── fifo_mem.v
│   └── fifo_diag.v
│
├── tb/
│   ├── tb_async_fifo_basic.v
│   └── fault_inject_tb.v
│
├── docs/
│   ├── block_diagram.png
│   ├── waveform_normal.png
│   ├── waveform_fault_injection.png
│   └── project_report.pdf
│
├── results/
│
├── README.md
├── LICENSE
└── .gitignore
