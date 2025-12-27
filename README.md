# 32-bit 5-Stage Pipelined RISC-V Processor

## 📋 Project Overview
A complete implementation of a 32-bit 5-stage pipelined RISC-V processor supporting the RV32I ISA, designed and verified as part of the Computer Architecture course at Namal University, Mianwali.

**Key Features:**
- 5-stage pipeline: IF, ID, EX, MEM, WB
- 28+ RISC-V RV32I instructions implemented
- Hazard detection and forwarding unit
- Static branch prediction
- Verilog implementation with ModelSim verification
- CPI analysis and performance evaluation

## 🏗️ Architecture
### Pipeline Stages
1. **IF (Instruction Fetch)** - Fetches instructions from memory using PC
2. **ID (Instruction Decode)** - Decodes instructions and reads register file
3. **EX (Execute)** - Performs ALU operations and branch resolution
4. **MEM (Memory Access)** - Handles load/store operations
5. **WB (Write Back)** - Writes results back to register file

### Instruction Support
| Type | Instructions |
|------|-------------|
| **R-type** | add, sub, and, or, xor, sll, srl, sra, slt |
| **I-type** | addi, ori, xori, andi, slli, srli, srai, slti |
| **Load/Store** | lw, sw, lb, sb, lh, sh |
| **Branch/Jump** | beq, bne, jal |
| **U-type** | lui, auipc |

## ⚙️ Key Components
### 1. Hazard Handling
- **Data Hazards**: Forwarding from EX/MEM and MEM/WB stages
- **Control Hazards**: Static branch prediction (always not-taken) with 1-cycle stall on misprediction
- **Load-Use Hazards**: Detection and stall insertion via Hazard Detection Unit

### 2. Forwarding Unit
- EX → EX forwarding (ALU result from previous instruction)
- MEM → EX forwarding (Result from load/store operations)
- Eliminates RAW hazards for back-to-back ALU operations

### 3. Performance Metrics
- **CPI**: 1.9 for test program (with optimized forwarding)
- **Clock Frequency**: Designed for 4 GHz (250ps clock period)
- **Pipeline Efficiency**: Verified through waveform analysis


## 🧪 Verification & Testing
### Test Programs
The processor was validated using comprehensive test programs covering:
1. **Basic Arithmetic** - R-type operations (add, sub, and, or)
2. **Immediate Operations** - I-type instructions (addi, xori)
3. **Memory Access** - Load/store operations (lw, sw)
4. **Control Flow** - Branch and jump instructions (beq, jal)
5. **Hazard Scenarios** - Data dependencies and forwarding verification

### Simulation Results
- **Waveform Analysis**: Verified pipeline flow, forwarding, and hazard handling
- **CPI Calculation**: Achieved 1.9 CPI for mixed workload
- **Functional Verification**: All 28+ instructions executed correctly

## 📊 Performance Analysis
| Metric | Value |
|--------|-------|
| Total Instructions | 10 |
| Total Cycles | 19 |
| CPI | 1.9 |
| Max Frequency | 4 GHz (assumed) |
| Pipeline Stages | 5 |
| Supported Instructions | 28+ |

## 🚀 Getting Started
### Prerequisites
- Verilog simulator (ModelSim/QuestaSim recommended)
- Basic understanding of RISC-V ISA and pipelining concepts

### Simulation
1. Clone the repository
2. Compile all Verilog files in ModelSim
3. Load the testbench (`PipelinedProcessor_tb.v`)
4. Run simulation for 1000ns
5. View waveforms for pipeline verification

### Test Program Example
```assembly
# Sample test program
add x3, x2, x1    # x3 = x2 + x1
sub x4, x2, x3    # x4 = x2 - x3
and x5, x3, x4    # x5 = x3 & x4
lw x9, 12(x2)     # Load from memory
beq x4, x3, 8     # Branch instruction
