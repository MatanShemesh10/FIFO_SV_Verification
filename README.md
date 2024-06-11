# FIFO Verification in SystemVerilog

This repository contains the implementation and verification of a FIFO (First-In-First-Out) buffer using SystemVerilog. This project was developed as part of a course on hardware verification.

## Project Overview

The goal of this project is to achieve full functional verification of a FIFO digital block in SystemVerilog. The FIFO acts as a buffer for data transfer between two synchronous and independent blocks. This repository includes the design, verification plan, testbench components, and the results of various tests performed on the FIFO.

## Directory Structure

- **src/**: Contains all source files, including the FIFO design and test classes.
- **tb/**: Includes all testbench components.
- **tests/**: Contains test files (program block with tests).
- **sim/**: Work directory for compiling and running simulations.

## DUT Specification

The Device Under Test (DUT) is a FIFO memory buffer with the following ports and parameters:

### Ports

| Name      | Width       | Direction | Description                                |
|-----------|-------------|-----------|--------------------------------------------|
| clk       | 1           | input     | Clock – triggers write/read operations     |
| reset     | 1           | input     | Asynchronous reset, active high            |
| rd_en     | 1           | input     | Read enable, active high                   |
| wr_en     | 1           | input     | Write enable, active high                  |
| data_in   | DATA_WIDTH  | input     | Data to be written into FIFO               |
| data_out  | DATA_WIDTH  | output    | Data read from FIFO                        |
| empty     | 1           | output    | FIFO empty flag, active high               |
| full      | 1           | output    | FIFO full flag, active high                |

### Parameters

| Name           | Values        | Default Value | Description                               |
|----------------|---------------|---------------|-------------------------------------------|
| DATA_WIDTH     | 8, 16, 32     | 8             | Memory data width                         |
| ADDRESS_WIDTH  | 4, 5, 6       | 4             | Log2 of memory capacity (16, 32, or 64 words) |

## Features Verified

The following features of the FIFO are verified:

- **Reset**: FIFO goes to initial state and its outputs go low at the first clock’s rising edge.
- **Write Operation**: Data is written into the FIFO at the rising clock edge if `wr_en` is active.
- **Read Operation**: Data is read from the FIFO at the rising clock edge if `rd_en` is active.
- **Full and Empty Flags**: Indicate the status of the FIFO.
- **Assertions**: Ensure that output signals do not get 'X' values and that there are no glitches on the signals.
- **Coverage**: Achieve 100% coverage by running all tests in regression and identifying coverage holes.

## Verification Environment

The verification environment consists of:

- **Driver**: Drives inputs to the FIFO.
- **Interface**: Groups functionally related signals.
- **Monitor**: Observes and records signal changes.
- **Sequence**: Generates inputs for the FIFO.
- **Sequencer**: Manages the flow of transactions.
- **Scoreboard**: Compares expected and actual results.

## Tests

The following tests were performed:

- **Reset Test**: Verifies the behavior of the FIFO upon reset.
- **Full Flag Test**: Ensures that data cannot be written when the FIFO is full.
- **Empty Flag Test**: Ensures that data cannot be read when the FIFO is empty.
- **Parallel Test**: Simultaneously writes and reads data.
- **Random Test**: Randomly performs read/write operations to ensure consistent behavior.

## Results

All tests were executed successfully, and the results are available in the `results` directory. The tests demonstrate that the FIFO operates correctly under various conditions and scenarios.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
