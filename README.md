# Automatic Door Controller Logic Using Verilog HDL

A simple combinational-logic project that controls an automatic door using two inputs:

- `person`: HIGH (`1`) when a person is detected.
- `safety`: HIGH (`1`) when the door area is safe.
- `door_open`: HIGH (`1`) to command the door to open.

The door opens only when **both** inputs are HIGH.

## Logic design

Boolean expression: `door_open = person & safety`

| person | safety | door_open |
|:------:|:------:|:---------:|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

## Project structure

```text
automatic-door-controller-verilog/
├── README.md
├── .gitignore
├── src/
│   ├── automatic_door_gate.v
│   └── automatic_door_dataflow.v
├── testbench/
│   └── tb_automatic_door.v
└── docs/
    └── waveform-notes.md
```

## Verilog implementations

- **Gate-level modelling:** uses an AND gate primitive.
- **Data-flow modelling:** uses a continuous `assign` statement.

The testbench below instantiates the gate-level module. To test the data-flow version, change `automatic_door_gate` to `automatic_door_dataflow` in the testbench.

## Run in EDA Playground

1. Open https://www.edaplayground.com/.
2. Select Verilog and a simulator such as Icarus Verilog.
3. Paste one design file from `src/` into the Design pane.
4. Paste `testbench/tb_automatic_door.v` into the Testbench pane.
5. Enable waveform/VCD output if required, then run.
6. Open the waveform and inspect `person`, `safety`, and `door_open`.

## Run locally with Icarus Verilog

From the project root:

```bash
iverilog -g2012 -o door_sim src/automatic_door_gate.v testbench/tb_automatic_door.v
vvp door_sim
gtkwave dump.vcd
```

For the data-flow model, replace `src/automatic_door_gate.v` with `src/automatic_door_dataflow.v`.

## Expected simulation results

| Time | person | safety | door_open |
|-----:|:------:|:------:|:---------:|
| 0 ns | 0 | 0 | 0 |
| 10 ns | 0 | 1 | 0 |
| 20 ns | 1 | 0 | 0 |
| 30 ns | 1 | 1 | 1 |
| 40 ns | 0 | 0 | 0 |

`door_open` should be HIGH only from 30 ns to 40 ns in this test sequence.

## Features

- Gate-level and data-flow Verilog descriptions.
- Testbench covers all four possible input combinations.
- `$monitor` prints signal values.
- `$dumpfile` and `$dumpvars` generate a VCD waveform file.

## Applications

- Automatic entrance-door control demonstrations.
- Digital logic and Verilog HDL laboratory exercises.
- Introductory FPGA/RTL simulation practice.

## Safety note

This is an educational logic model, not a complete real-world door safety controller. A physical installation needs suitable sensors, motor/driver circuitry, obstruction detection, emergency/manual controls, fault handling, and a properly engineered safety system.

## Author

R.prawin, ece ,mahendra engineering college
