A high-performance, pipelined Posit Multiplier implemented on the Xilinx Artix-7 FPGA (xc7a35tcpg236-1). This project provides a comparative analysis between the emerging Posit number system and the standard IEEE 754 floating-point format.

 Introduction 
The Posit number system offers a dynamic bit allocation strategy, allowing for higher precision near 1.0 and a larger dynamic range than IEEE 754 for the same bit width. This project focuses on the hardware realization of a 32-bit Posit multiplier.

 Key Features
* **Target Device:** Xilinx Artix-7 (Basys 3 / xc7a35tcpg236-1).
* **Architecture:** 3-stage pipelined execution.
* **Performance:** Optimized for high frequency using DSP48 slices.
* **Comparison:** Benchmarked against IEEE 754 standard for resource utilization and power.


## 🏗 Methodology & Architecture
The multiplier is designed in three distinct pipeline stages to maximize throughput:

1.  **Stage 1: Decode (Extraction)**
    * Extracts regime bits using a **Leading Zero/One Detector (LZOD)**.
    * Separates the sign, exponent, and fraction fields.
2.  **Stage 2: Execution (Core Computation)**
    * XOR logic for the output sign.
    * Scale factor computation via adder logic.
    * Mantissa multiplication ($1.f_A \times 1.f_B$) utilizing **FPGA DSP48 slices**.
3.  **Stage 3: Encode (Packing)**
    * Normalization and rounding of the product.
    * Re-packing into the final 32-bit Posit format.

---

## 📊 Implementation Results
The following results were obtained after Synthesis and Implementation in Vivado for the `xc7a35tcpg236-1`.

### Timing & Performance
The following performance metrics were achieved after implementation:

| Metric | Value |
| :--- | :--- |
| **Max Frequency** | 542.59 MHz |
| **WNS (Worst Negative Slack)** | 8.157 ns |

### Resource Utilization
The following resources were utilized on the **Artix-7 (xc7a35tcpg236-1)**:

| Resource | Used | Available | Utilization % |
| :--- | :--- | :--- | :--- |
| **LUT** | 2207 | 20800 | 10.61% |
| **FF** | 2492 | 41600 | 5.99% |
| **DSP** | 4 | 90 | 4.44% |
| **IOB** | 1 | 106 | 0.94% |

### Power Analysis
* **Total On-Chip Power:** 0.08 W
* **Junction Temperature:** 25.4°C



## 📉 Comparison: Posit vs. IEEE 754
Our findings indicate that the Posit Multiplier provides:
* **Better Accuracy:** Higher precision for values close to unity.
* **Dynamic Range:** Superior range-to-bit ratio.
* **Hardware Trade-off:** Slight increase in LUT utilization due to the variable-length regime decoding compared to the fixed fields of IEEE 754.



## 🛠 Setup & Usage
1.  **Environment:** Xilinx Vivado 2022.2 .
2.The project implementation can be done in VIVADO by the following steps:
   a.Uploading the design source files namely, posit_multiplier.v and fp_benchmark_top.v
   b.Uploading the testbench files namely,posit_multiplier_tb.v under simulation sources
   c.Uploading the appropriate constraints file(.xdc) file
   d.Depending on whichever we want whether the floating point multiplier to be synthesised or the posit multiplier to be synthesised we set either of the files as top using the 'Set as Top' instruction by right clicking on the file in vivado.
   e.Then Running synthesis and implementation will help us to run the project

## 👥 Team Members
* **Akshat Mittal** (IMT2023606)
* **Nachiappan** (IMT2023605)
   
