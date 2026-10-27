# CLTUForge Pro (v1.0.0)

### CCSDS 231.0-B-4 & ISO 12172 TC Channel Coding & Command Link Transmission Unit (CLTU) Studio

CLTUForge Pro is an aerospace-grade developer studio, Command Link Transmission Unit (CLTU) synthesizer, Modified BCH (63, 56\) forward error correction encoder/decoder, PLOP-1/PLOP-2 carrier modulation sequencer, and 10-point normative compliance auditor designed for spacecraft flight software teams, ground station engineers (NASA DSN, ESA ESTRACK, KSAT, MBRSC UAE), and commercial mission operators (Artemis lunar landers, Earth-observation CubeSats, Mars exploration rovers).

---

## 🌟 Key Capabilities

- **Normative CLTU Synthesis (CCSDS 231.0-B-4)**: Generates bit-exact Command Link Transmission Units combining the 16-bit Start Sequence (`0xEB90`), arbitrary length Modified BCH (63, 56\) codeblocks, and the normative 64-bit Tail Sequence (`0xC5C5C5C5C5C5C579`).  
- **Modified BCH (63, 56\) Polynomial Codec**: Implements generator polynomial \$g(x) \= x^7 \+ x^6 \+ x^2 \+ 1\$ with 56-bit information chunking, 7-bit parity remainder calculation, trailing bit inversion enforcement, and single-bit error detection/correction.  
- **Tail Sequence & Abort Verification**: Mathematical verification of deliberate abort syndrome \$S \= \\text{0x3C}\$ to ensure clean spacecraft telecommand decoder termination without frame sync slip.  
- **Physical Layer Operations Procedures (PLOP)**: Implements PLOP-1 (discontinuous carrier keying) and PLOP-2 (continuous carrier keying) with 16-octet Acquisition Sequences (`0x55`) and Idle Fill sequences.  
- **Single-Bit Error Correction & Syndrome Dissector**: Features an automated syndrome lookup table mapping all 63 distinct error bit indices to enable ground verification of uplink decoder resilience.  
- **10-Point Normative Compliance Auditor**: Automated test and verification engine enforcing rules `CLTU-001` through `CLTU-010`.

---

## 📂 Project Structure

cltu-forge-pro/

├── source-code/

│   ├── cltu-engine.js           \# Core BCH 63/56 codec, CLTU assembler & PLOP engine

│   ├── cltu-auditor.js          \# 10-point normative compliance auditor

│   ├── cltu\_cli.py              \# Pure Python 3 CLI executable

│   ├── cltu-cli.py              \# Pure Python 3 CLI alias

│   ├── test\_runner.py          \# 10-suite unit test runner

│   └── index.html               \# Interactive Mission Control operations console

├── build/

│   └── cltu-forge-pro-v1.0.0.zip \# Standalone production bundle

├── documentation/

│   ├── CCSDS\_CLTU\_SPECIFICATION.md \# Normative protocol specification

│   └── CLTU\_COMPLIANCE\_MATRIX.md   \# 10-point requirement traceability

└── screenshots/

    ├── architecture-diagram.svg  \# System architecture diagram

    └── cltu-studio-preview.svg    \# Operations console preview

---

## 🚀 Quick Start

### Running Automated Tests

python3 source-code/test\_runner.py \-v

### Command Line Interface

\# Synthesize standard CLTU from telecommand payload

python3 source-code/cltu\_cli.py \--mode cltu \--payload "THRUSTER\_FIRING\_1200MS"

\# Synthesize CLTU and inject a correctable 1-bit error for decoder testing

python3 source-code/cltu\_cli.py \--mode cltu \--payload "LEOP\_DEPLOY\_SOLAR\_ARRAY" \--inject-error-bit 12

\# Decode a raw hex CLTU and recover telecommand frame

python3 source-code/cltu\_cli.py \--mode decode \--payload "BURN\_CMD"

\# Run 10-Point Normative Compliance Audit on synthesized CLTU

python3 source-code/cltu\_cli.py \--mode audit \--payload "CRITICAL\_BURN\_TELECOMMAND"

\# Generate PLOP-2 continuous carrier acquisition and idle stream

python3 source-code/cltu\_cli.py \--mode plop \--plop-mode PLOP-2

### Launching the Web Operations Console

Open `source-code/index.html` in any web browser to access the interactive Mission Control dashboard, visual CLTU synthesizer, codeblock dissector, and 10-point compliance scorecard.