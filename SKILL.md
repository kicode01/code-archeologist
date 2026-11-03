---
name: code-archeologist
description: >-
  [WHAT IT DOES]: Reverse-engineers, decompiles, and modernizes mission-critical legacy codebases
  (COBOL, Fortran, Ada, C89, or closed-source binaries) into verified, memory-safe Rust or WebAssembly (WASM).
  [WHEN TO USE]: Use when modernizing unmaintained legacy systems, porting proprietary binaries or ancient libraries,
  fixing memory vulnerabilities without altering business rules, or rescuing systems from dying hardware architectures.
  [WHEN NOT TO USE]: Do NOT use for basic JavaScript framework upgrades or greenfield web application scaffolding.
---

# Code Archeologist: Legacy Modernizer & MicroVM Sandboxer

```
  +---------------------------------------------------------------------------------+
  |                               CODE ARCHEOLOGIST                                 |
  |         Legacy Decompilation, Wasm MicroVM & Differential Fuzzing               |
  +---------------------------------------------------------------------------------+

  [Legacy Artifact (COBOL/Fortran/C89/Binary)]
                        |
                        v
          [Control Flow & Memory Decompilation]
          - Linear Memory Boundaries
          - Endianness & Register Bit-Width Extraction
          - Implicit Wrap-Around Arithmetic Detection
                        |
                        v
        +---------------+---------------+
        |                               |
        v                               v
  [Legacy Execution Engine]    [Modernized Rust / WASM MicroVM]
        |                               |
        +---------------+---------------+
                        |
                        v
       [Mutation-Based Differential Fuzzer]
       - Bit Flips & Byte Swaps
       - Integer Boundary Injections
       - Thousands of Parallel Stress Cycles
                        |
        +---------------+---------------+
        |                               |
  [Divergence Discovered]          [100% Bit Parity]
        v                               v
  [Emit Counterexample Payload]   [Export Zero-Dependency WASM]
  - Disclose Implicit Hardware    - Micro-Second Cloud MicroVM
    Quirks to Engineer            - Provable Safety Guarantee
```

---

## 1. When to Activate

Trigger `code-archeologist` when:
- **Legacy Systems Modernization:** Moving 30-year-old COBOL, Fortran, or C89 routines to modern cloud architectures.
- **Rescuing Abandoned Binaries:** Porting closed-source `.dll` or `.so` libraries whose original compilers or source repositories were lost.
- **Memory Safety Hardening:** Eliminating buffer overflows and dangling pointer CVEs from critical infrastructure without altering business logic.
- **Hardware Architecture Emulation:** Porting legacy software running on retired CPUs (M68k, SPARC, Alpha, PowerPC) into portable WebAssembly.

---

## 2. Modernization & Transpilation Runbook

### Step 1: Decompilation & Semantic Reconstruction
1. Map global memory banks, struct alignment offsets, and pointer arithmetic patterns.
2. Identify architecture-specific implicit quirks:
   - 16-bit or 32-bit integer overflow wrapping.
   - Fixed-point decimal arithmetic (common in COBOL financial engines).
   - Endianness dependencies (Big-Endian vs Little-Endian byte ordering).

### Step 2: Rust / WebAssembly MicroVM Scaffolding
Use [wasm_scaffold.rs](./templates/wasm_scaffold.rs) to wrap linear memory into safe, bounds-checked Rust vectors targeting `wasm32-wasi`:
```rust
let mut vm = LegacyMemoryState::new();
let result = vm.execute_cycle(&input_payload);
```

### Step 3: Run Differential Fuzzing
Execute the differential test engine across millions of mutated payloads:
```bash
python scripts/differential_fuzzer.py --demo
```
- The mutation engine injects boundary values, integer extremes, and bit-flips.
- Compares return codes, standard output, and memory side effects between the legacy binary and modern WASM code.

### Step 4: Safe Containerized Cloud Export
Package the verified WASM module into a standalone container microservice runnable on Cloudflare Workers, AWS Lambda, Kubernetes, or Vercel Serverless.

---

## 3. Reference Files
- [differential_fuzzer.py](./scripts/differential_fuzzer.py): Differential testing and mutation engine.
- [wasm_scaffold.rs](./templates/wasm_scaffold.rs): Bounds-checked memory-safe Rust/WASM scaffold.
