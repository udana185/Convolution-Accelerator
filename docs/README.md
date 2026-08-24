# Convolution-Domain Hardware Accelerator with RV32I Integration

An ongoing hardware design project exploring how to accelerate convolution
operations — as used in image and signal processing (e.g. filtering, edge
detection, blurring) — directly in hardware, tightly coupled to an RV32I
(RISC-V) CPU through shared on-board memory (BRAM).

## Motivation

Convolution operations are computationally repetitive and well suited to
dedicated hardware, but running them purely in software on a general-purpose
processor is slow. This project explores offloading the convolution itself to
a dedicated hardware accelerator, while keeping the RV32I CPU in the loop for
control, data staging, and any non-accelerated processing — a common
architecture pattern for embedded signal/image processing systems.

## Approach

The design is being built incrementally rather than attempted all at once:

1. **Stepping stone: RV32I CPU + BRAM + simple multiplier accelerator.**
   The RV32I core and the FPGA's on-board Block RAM (BRAM) are paired with a
   basic hardware multiplier accelerator, to validate the CPU–accelerator–
   memory communication pattern before adding complexity.
2. **Target: convolution-domain accelerator.** The multiplier accelerator is
   extended into a dedicated convolution engine, sharing BRAM with the RV32I
   core so both can access input/output data without costly transfers.

## Architecture (current / planned)

- **Core:** RV32I RISC-V CPU (existing open source core for first implementation)
- **Accelerator:** [add: MAC array size / kernel size supported / structure],
  memory-mapped and controlled from the RV32I core
- **Memory:** Shared on-board BRAM, accessible by both CPU and accelerator,
  (dual port memory access)
- **Toolchain:** SystemVerilog, [Quartus Prime / ModelSim] for simulation and
  synthesis, targeting [Altera DE2 Board]

## Status

🚧 Work in progress. The multiplier-accelerator stepping stone (RV32I CPU +
BRAM + multiplier) is [in progress], with the
full convolution-domain accelerator to follow.

## Roadmap

- [ ] Finish and verify RV32I CPU + BRAM + multiplier accelerator baseline
- [ ] Define convolution accelerator datapath and BRAM-sharing interface
- [ ] Implement and simulate convolution accelerator in SystemVerilog
- [ ] Synthesize and test on FPGA hardware
- [ ] Benchmark against software-only convolution on the RV32I core

## Author

Udana Athukorala — Electronic & Telecommunication Engineering, University of
Moratuwa
