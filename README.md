# BabySoC – Week 2: Fundamentals & Functional Modelling

## Objective
Build a solid understanding of SoC fundamentals and practice functional modelling of BabySoC using Icarus Verilog and GTKWave.

## Project Overview
VSDBabySoC integrates three main modules:
- **RISC-V Processor (rvmyth)**: Generates 10-bit digital output.
- **PLL Module (avsdpll)**: Provides a stable clock for the SoC.
- **DAC Module (avsddac)**: Converts digital output to analog signal.

Testbench (`testbench.v`) simulates the complete SoC and generates waveform files for analysis.

## Directory Structure
VSDBabySoC/
├── src/              # Verilog source files and headers
├── output/           # Simulation outputs
│   ├── pre_synth_sim/
│   └── post_synth_sim/
├── screenshots/      # GTKWave screenshots
└── docs/
    └── Observations.md

## Simulation Steps

### Pre-Synthesis
mkdir -p output/pre_synth_sim
iverilog -o output/pre_synth_sim/pre_synth_sim.out -DPRE_SYNTH_SIM -I src/include -I src/module src/module/testbench.v src/module/vsdbabysoc.v
cd output/pre_synth_sim
./pre_synth_sim.out
gtkwave pre_synth_sim.vcd

### Post-Synthesis
mkdir -p output/post_synth_sim
iverilog -o output/post_synth_sim/post_synth_sim.out -DPOST_SYNTH_SIM -I src/include -I src/module src/module/testbench.v output/synthesized/vsdbabysoc.synth.v
cd output/post_synth_sim
./post_synth_sim.out
gtkwave post_synth_sim.vcd

## Observations
Detailed waveform analysis is in `docs/Observations.md`. Key aspects:
- Reset Operation
- Clocking
- Dataflow from RISC-V to DAC

## Tools Used
- Icarus Verilog (iverilog)
- GTKWave

## Author
Tejasri Aluri
