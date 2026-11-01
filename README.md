# 4-bit Synchronous Loadable Mod-12 Up-Down Counter Verification

A comprehensive **SystemVerilog (SV)** based verification environment for a 4-bit Synchronous Loadable Mod-12 Up-Down Counter, achieving **100% Functional Coverage**.

---

## 📋 Design Specification

- **Design**: 4-bit Synchronous Loadable Mod-12 Up-Down Counter
- **Counting Range:**
  - Up Count: 0 to 11 (wraps to 0)
  - Down Count: 11 down to 0 (wraps to 11)
- **Functionality:** Supports up counting, down counting, parallel load, and active-low asynchronous/synchronous reset.

### Control Mechanisms
* `resetn = 0`: Counter resets to `0`.
* `load = 1`: Loads custom data from `data_in[3:0]`.
* `up_down = 1`: Up counting mode.
* `up_down = 0`: Down counting mode.

---

## 🔌 Port List

| Port Name | Direction | Width | Description |
| :--- | :---: | :---: | :--- |
| `clock` | Input | 1-bit | System clock signal |
| `resetn` | Input | 1-bit | Active-low reset signal |
| `load` | Input | 1-bit | Parallel load enable signal |
| `up_down` | Input | 1-bit | Direction control (1 = Up, 0 = Down) |
| `data_in` | Input | 4-bit | Parallel load data input |
| `count` | Output | 4-bit | Counter output state |

---

## 🛠️ Verification Environment & Tools
* **Language:** SystemVerilog (SV)
* **Simulators:** QuestaSim / VCS / Vivado
* **Achievement:** **100% Functional Coverage** & Code Coverage
* **Automation:** Makefile-based simulation and regression flow

---

## 🏗️ Testbench Architecture & Topology

The verification environment follows a structured, modular Object-Oriented / Module-based SystemVerilog methodology:

1. **Interface:** Bundles all DUV (Design Under Verification) signals and connects the testbench components with the design using virtual interfaces / modports.
2. **Generator / Sequence:** Creates randomized transaction packets (`resetn`, `load`, `up_down`, `data_in`) and sends them to the driver.
3. **Driver:** Receives transactions and drives them onto the DUV signals.
4. **Write Monitor:** Observes input signals applied to the DUV and sends captured input transactions to the reference model.
5. **Read Monitor:** Observes DUV output (`count`) and sends actual output to the scoreboard.
6. **Reference Model:** Computes expected counter outputs based on the specification and forwards them to the scoreboard.
7. **Scoreboard:** Compares data received from the reference model and read monitor, reporting **PASS** on matches and **FAIL** on mismatches.

---

## 🎯 Test Cases & Coverage

* **Reset Test (TC1):** Verifies that applying active-low reset immediately clears the counter output to `0`.
* **Parallel Load Test (TC2):** Checks that when `load = 1`, custom input values from `data_in[3:0]` are correctly loaded into the counter.
* **Up/Down Counting Tests (TC3):** Verifies sequential counting from `0` to `11` (Up) and `11` to `0` (Down) with smooth wrap-arounds.
* **Random Test:** Randomly applies control inputs to verify overall robustness and corner-case functionality.

---

## 📝 Project Summary

* Developed a robust, automated verification environment using **SystemVerilog** for a custom Mod-12 Up-Down Counter.
* Implemented modular testbench components including independent transaction generators, drivers, monitors, a golden reference model, and an automated self-checking scoreboard.
* Achieved **100% Functional Coverage** and comprehensive code coverage across all control states (Reset, Load, Up-counting, and Down-counting boundary conditions).
* Established a streamlined **Makefile-based regression and automated HTML coverage reporting flow** compatible with industry-standard EDA tools (QuestaSim/VCS).

---

## 🚀 Future Improvements

* **UVM Migration:** Transitioning the pure SystemVerilog testbench architecture into **UVM (Universal Verification Methodology)** to leverage standard phases, sequences, and reusable factory components.
* **Assertion-Based Verification (ABV):** Integrating SystemVerilog Assertions (SVA) inside interface or design files to check protocol compliance and temporal properties dynamically (e.g., checking that max count never exceeds 11 and illegal states are avoided).
* **Coverage-Driven Closure:** Expanding functional coverage bins with specialized cross-coverage points (e.g., cross-coverage between `load` transitions and `up_down` states during peak roll-over conditions).
* **CI/CD Integration:** Automating regression runs and coverage report generation via GitHub Actions for continuous verification.

---

## 🚀 Usage (Makefile Targets)

```bash
make clean          # Clean earlier logs and intermediate files
make sv_cmp         # Create library and compile the code
make TC1            # Run Testcase 1 in batch mode
make TC2            # Run Testcase 2 in batch mode
make TC3            # Run Testcase 3 in batch mode
make regress_12     # Run regression for TC1 and TC2
make report_12      # Merge coverage reports and convert to HTML
make covhtml        # View coverage report in browser
```
---

# 👤 Author
## Mo. Aslam Chaudhary
---
* B.Tech: Electronics and Communication Engineering
* Focus: VLSI Design & Design Verification
