\# Hardware Acceleration of ChaCha20 and ASCON Ciphers on a RISC-V Softcore Using Custom Instructions



\## Project Overview



This project focuses on the hardware acceleration of the ChaCha20 and ASCON cryptographic algorithms on a RISC-V softcore processor using custom instructions.



The project investigates a tightly coupled instruction-level acceleration approach in which computationally intensive cryptographic operations are implemented as custom RISC-V instructions and integrated with the CVA6/CV32A6 processor through the Core-V eXtension Interface (CV-X-IF).



The implementation is intended for deployment on a Xilinx Zynq-7000 FPGA platform.



\## Problem Statement



ChaCha20 and ASCON are lightweight cryptographic algorithms suitable for resource-constrained embedded systems such as satellites, IoT devices, and sensor networks.



However, executing these algorithms purely in software on a general-purpose 32-bit RISC-V processor can result in high cycle counts per encrypted bit.



This project addresses this issue by implementing custom RISC-V instructions for frequently executed cryptographic operations and integrating them with the CVA6/CV32A6 softcore through CV-X-IF.



In addition to performance evaluation, the project also investigates the power and energy consumption of the extended coprocessor.



\## Objectives



\- Implement a pure-software baseline of ChaCha20 and ASCON on a CV32A6 RISC-V softcore deployed on an FPGA.

\- Measure baseline cycles/bit and instructions/bit.

\- Design and integrate custom RISC-V instructions for cryptographic operations.

\- Integrate the custom instructions into the CV32A6 coprocessor through the CV-X-IF interface.

\- Validate the performance improvement against the pure-software baseline.

\- Analyze hardware cost including LUTs, flip-flops, and estimated gate equivalent cost.

\- Characterize power and energy consumption of the extended coprocessor.

\- Evaluate the performance-to-power trade-off.



\## Proposed Methodology



The project follows the following development flow:



1\. Baseline benchmarking

2\. Algorithmic profiling

3\. Custom instruction design and encoding

4\. Hardware integration through CV-X-IF

5\. Re-benchmarking and validation

6\. Power and energy characterization



\## Processor Platform



\### CVA6 / CV32A6



The project uses the CVA6/CV32A6 RISC-V softcore.



Key characteristics:



\- 32-bit RISC-V processor

\- 6-stage processor architecture

\- Open-source processor core

\- Developed by the OpenHW Group

\- Intended for FPGA and ASIC implementations



\## Cryptographic Algorithms



\### ChaCha20



ChaCha20 is a stream cipher based on the ARX operations:



\- Addition

\- Rotation

\- XOR



The project focuses on identifying frequently executed operations in the ChaCha20 Quarter Round that can benefit from custom hardware instructions.



\### ASCON



ASCON is a lightweight authenticated encryption and hashing algorithm.



The project investigates the substitution and diffusion operations of ASCON for possible hardware acceleration.



\## Custom RISC-V Instructions



The project implements and evaluates the following custom instructions:



\### R-type Instructions



\- ROR64H

\- ROR64L

\- MROR64H

\- MROR64L



\### R4-type Instructions



\- OP\_CHACHA

\- OP\_ASCON



These instructions are intended to accelerate computationally intensive operations in ChaCha20 and ASCON.



\## CV-X-IF Integration



The custom instructions are integrated with the CVA6/CV32A6 processor through the Core-V eXtension Interface (CV-X-IF).



The CV-X-IF interface provides a mechanism for connecting an external coprocessor to the RISC-V processor and supporting custom instruction execution.



The objective is to integrate the cryptographic acceleration without modifying the main processor pipeline.



\## FPGA Implementation



The target FPGA platform specified for the project is:



\- Xilinx Zynq-7000

\- Zybo Z7-20 development board



The hardware implementation will be developed and evaluated using Xilinx Vivado.



\## Performance Evaluation



The accelerated implementation will be compared with the pure-software baseline using:



\- Clock cycles

\- Cycles per bit

\- Instructions per bit

\- Performance speedup

\- Hardware resource utilization



Compiler optimization levels such as -O1, -O2, and -O3 will also be considered during benchmarking.



\## Power and Energy Characterization



The project extends the evaluation beyond performance by characterizing:



\- FPGA/coprocessor power consumption

\- Energy consumption

\- Performance-to-power trade-off



This provides additional information for evaluating the suitability of the accelerator in power-constrained embedded and space-oriented applications.



\## Repository Structure



```text

CVA6/

&#x20;   CVA6 processor source and related implementation



Crypto/

&#x20;   ChaCha20 and ASCON software/hardware implementation



Simulation/

&#x20;   Simulation files, testbenches and simulation results



Results/

&#x20;   Performance, hardware resource, power and energy results



README.md

&#x20;   Project documentation



.gitignore

&#x20;   Files excluded from Git tracking

\---



\## Tools and Technologies



\### Hardware



\- CVA6/CV32A6 RISC-V softcore

\- Xilinx Zynq-7000 FPGA

\- Zybo Z7-20 development board



\### Software and Development Tools



\- Xilinx Vivado

\- RISC-V GNU GCC toolchain

\- SystemVerilog

\- Bare-metal RISC-V development environment

\- Inline assembly



\### Interface



\- Core-V eXtension Interface (CV-X-IF)



\---



\## Current Project Status



\### Completed



\- Project scope and methodology defined.

\- RISC-V GNU GCC toolchain installed.

\- RISC-V GCC toolchain verified successfully on Windows.

\- Git repository initialized locally.

\- Public GitHub repository created.

\- Project README and `.gitignore` created.



\### In Progress



\- CVA6/CV32A6 environment setup.

\- Study and setup of the CV-X-IF interface.

\- Pure-software ChaCha20 and ASCON baseline implementation.

\- Baseline performance benchmarking.

\- Algorithmic profiling.

\- Custom instruction design.

\- Cryptographic coprocessor implementation.



\### Planned



\- Integration of the custom coprocessor through CV-X-IF.

\- FPGA synthesis and implementation.

\- Performance comparison between software and hardware-accelerated implementations.

\- Hardware resource analysis.

\- Ablation study of individual custom instructions.

\- Power and energy characterization.

\- Performance-to-power trade-off analysis.

\- Final validation and documentation.



\---



\## Expected Outcomes



The project aims to achieve the following outcomes:



\- A working CV32A6-based implementation of ChaCha20 and ASCON.

\- Integration of six custom cryptographic instructions.

\- A functional cryptographic coprocessor connected through CV-X-IF.

\- FPGA implementation of the extended processor.

\- Independent performance evaluation against the pure-software baseline.

\- Measurement of cycles per bit and instructions per bit.

\- Hardware resource utilization analysis.

\- Power and energy characterization.

\- Performance-to-power trade-off analysis.



The evaluation will target the performance improvements reported in the reference work while independently validating the results on the selected FPGA platform.



\---



\## System Architecture



The proposed system consists of the following major components:



```text

&#x20;                +----------------------+

&#x20;                |      RISC-V          |

&#x20;                |    CVA6 / CV32A6     |

&#x20;                +----------+-----------+

&#x20;                           |

&#x20;                           | CV-X-IF

&#x20;                           |

&#x20;                +----------v-----------+

&#x20;                | Cryptographic        |

&#x20;                | Coprocessor           |

&#x20;                +----------+-----------+

&#x20;                           |

&#x20;                +----------+-----------+

&#x20;                |                      |

&#x20;         +------v------+        +------v------+

&#x20;         |  ChaCha20   |        |   ASCON     |

&#x20;         | Acceleration|        | Acceleration|

&#x20;         +-------------+        +-------------+

&#x20;                           |

&#x20;                    FPGA Platform

&#x20;                           |

&#x20;                 +---------v---------+

&#x20;                 |  Zynq-7000 /      |

&#x20;                 |  Zybo Z7-20       |

&#x20;                 +-------------------+

