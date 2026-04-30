<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=2d3a1f&height=140&section=header&text=Decoding%20the%20Unknown&fontSize=42&fontColor=f5f0e8&fontAlignY=38&desc=Binary%20Analysis%20%E2%80%A2%20Decompilation%20Research%20%E2%80%A2%20Systems%20Engineering&descSize=16&descAlignY=62"/>

<br>

<div align="center">
  <img src="Deisgn%20Knowkill.png" width="100%" style="max-width:900px"/>
</div>

<br>

<div align="center">

[![Typing SVG](https://readme-typing-svg.herokuapp.com/?color=6b7c3a&size=22&center=true&vCenter=true&width=900&lines=Independent+Security+Researcher;Founder+of+@AkashaCorporation;Building+Helix+—+MLIR+Decompiler;Building+HexCore+—+Binary+Analysis+IDE;Where+Software+Meets+Hardware)](https://git.io/typing-svg)

</div>

<br>

---

## About

I'm an **independent security researcher** and **systems engineer** from Brazil, working at the intersection of compiler infrastructure and binary analysis. My current research focuses on decompiler pipeline architecture, SSA-based variable recovery, and MLIR dialect design for reverse engineering.

I founded [**@AkashaCorporation**](https://github.com/AkashaCorporation) to build the next generation of reverse engineering tooling. My flagship project, **HikariSystem HexCore**, is an open-source binary analysis IDE with native engines for disassembly, emulation, and MLIR-based decompilation — battle-tested against real malware, kernel modules, and AAA game binaries.

---

## Research

<div align="center">

[![Paper](https://img.shields.io/badge/Paper-Helix%3A%20MLIR%20Decompilation%20with%20Pipeline%20Loss%20Analysis-2d3a1f?style=for-the-badge&logoColor=white)](#)

</div>

*"Helix: Multi-Level IR Decompilation via MLIR Dialect Lowering with Empirical Pipeline Loss Analysis"*

The first application of MLIR's multi-level dialect framework to binary decompilation. Through instrumented analysis of 70+ real-world functions across Linux kernel drivers, Windows PE game binaries, and CTF executables, the paper identifies that the primary decompilation quality bottleneck is at the **register-to-variable recovery boundary**, where a single-variable-per-register model causes cascading elimination of **99.7% of recovered assignments**.

Solutions: **SSA variable splitting** with reverse post-order traversal, **Ghidra-inspired type recovery**, and **SCC-based irreducible CFG detection**. Result: `kbase_jit_allocate` went from 14 lines to 133 lines (4.4% → 42.9% vs IDA Pro), with 0 crashes across 70 test files.

**Status:** Draft complete · Target venues: CC, CGO, USENIX Security

---

## Flagship Projects

### HikariSystem HexCore — Binary Analysis IDE

[![HexCore](https://img.shields.io/badge/HexCore-v3.8.0--nightly-2d3a1f?style=for-the-badge&logo=c%2B%2B&logoColor=white)](https://github.com/LXrdKnowkill/HikariSystem-HexCore)

A comprehensive open-source binary analysis IDE built as a fork of code-oss, providing a unified environment for malware analysis, reverse engineering, and threat hunting. Native engines for disassembly, emulation, decompilation, and patching — all running in-process via N-API bindings without external installations.

**Battle-tested against:** ARM Mali GPU kernel driver (`mali_kbase.ko`, 45MB, 7,313 functions), Rise of the Tomb Raider (Windows PE64), Riot Vanguard (anti-cheat), CTF binaries, and live malware samples with API hashing, anti-VM, and anti-debug.

**Stack:** TypeScript · C++23 · MLIR · LLVM 18.1.8 · Capstone · Unicorn · Remill · Z3 · Souper · Electron · Node.js N-API

<br>

### Helix — MLIR-based Decompiler Engine

[![Helix](https://img.shields.io/badge/Helix-v0.9.0-4a5a28?style=for-the-badge&logo=llvm&logoColor=white)](#)

C++23/MLIR pipeline with **19 analysis passes** organized into three custom dialects: **HelixLow** (machine-level), **HelixMid** (ISA-agnostic typed SSA), and **HelixHigh** (C-level constructs). The first decompiler built on MLIR's multi-level IR framework.

**v0.9.0 highlights:**
- 70/70 test files crash-free, 100% confidence on all functions
- SSA variable splitting with RPO + immediate dominator seeding
- Ghidra-inspired type recovery (44% typed parameters, from 0%)
- SCC-based irreducible CFG detection via Tarjan's algorithm
- Variable coalescing, dynamic array detection, alias analysis, RTTI class naming
- Per-function confidence scoring with quality penalties and bonuses

<br>

### Pathfinder — Pre-Lift CFG Recovery Engine

[![Pathfinder](https://img.shields.io/badge/Pathfinder-v0.2.0-6b7c3a?style=for-the-badge)](#)

A novel pre-lift CFG analysis engine using `.pdata`/`.symtab` boundaries, recursive descent disassembly, and jump table resolution to discover basic blocks and function boundaries before reaching the lifter. On `kbase_jit_allocate` (2,137 bytes), Pathfinder discovers **142 leaders from 479 instructions** — a level of pre-lift CFG visibility no existing decompiler provides.

<br>

### hexcore-souper — First Windows N-API Build of Google Souper

[![Souper](https://img.shields.io/badge/Souper-v0.2.0-3d4f21?style=for-the-badge)](#)

The **first Windows N-API port of Google Souper** with Z3 SMT solving. Makes Souper's superoptimization and constraint-solving accessible to Node.js applications on Windows. Empirical finding: near-zero impact on production binaries, but valuable for obfuscated/cryptographic analysis. Documented as a negative result — useful for the community to know.

<br>

### Project Azoth — Clean-Room Dynamic Analysis Framework

[![Azoth](https://img.shields.io/badge/Azoth-In%20Development-8a9a56?style=for-the-badge)](#)

A clean-room, Apache-2.0 licensed dynamic analysis framework in **Rust + C++23**. Four tiers: Unicorn-driven CPU emulation, multi-format binary loaders (PE/ELF/Mach-O), OS-level abstraction (Windows + Linux syscalls, API hooks, VFS, Registry, TEB/PEB), and Frida-style instrumentation with SharedArrayBuffer zero-copy event pipeline. **Designed to replace Qiling.**

---

## Engineering Achievements

| Achievement | Impact |
|---|---|
| **Helix MLIR pipeline** | First decompiler built on MLIR's multi-level dialect framework |
| **SSA variable splitting** | Resolved 99.7% assignment loss in decompiler dead-code elimination |
| **Pathfinder CFG engine** | Discovered 142 leaders in 2KB of kernel code (pre-lift) |
| **First Windows Souper port** | Google Souper + Z3 accessible from Node.js on Windows |
| **SAB zero-copy IPC** | Lock-free SharedArrayBuffer ring buffer eliminating 65% TSFN drop rate |
| **HEXCORE_DEFEAT v3 emulation** | 1M instructions executed, 23,128 API calls captured against custom anti-analysis malware |
| **Pipeline loss analysis methodology** | First per-stage operation survival data for any decompilation pipeline |
| **MSVC C++ data import handling** | Solved `std::cout` vbtable access in PE emulation |

---

## Technical Stack

<div align="center">

**Compiler & Systems**

[![Skills](https://skillicons.dev/icons?i=cpp,c,rust,go,asm,cmake&perline=6)](https://skillicons.dev)

**Binary Analysis & Reverse Engineering**

![MLIR](https://img.shields.io/badge/MLIR-1a2210?style=for-the-badge&logo=llvm&logoColor=white)
![LLVM](https://img.shields.io/badge/LLVM-1a2210?style=for-the-badge&logo=llvm&logoColor=white)
![Capstone](https://img.shields.io/badge/Capstone-2d3a1f?style=for-the-badge)
![Unicorn](https://img.shields.io/badge/Unicorn-2d3a1f?style=for-the-badge)
![Remill](https://img.shields.io/badge/Remill-2d3a1f?style=for-the-badge)
![Z3](https://img.shields.io/badge/Z3-2d3a1f?style=for-the-badge)
![Souper](https://img.shields.io/badge/Souper-2d3a1f?style=for-the-badge)

**Application & Web**

[![Skills](https://skillicons.dev/icons?i=nodejs,ts,electron,tauri,react,next&perline=6)](https://skillicons.dev)

**DevOps & Tools**

[![Skills](https://skillicons.dev/icons?i=git,github,docker,linux,windows,vscode&perline=6)](https://skillicons.dev)

</div>

---

## GitHub Stats

<div align="center">
  <img src="https://github-readme-stats-lime-ten-54.vercel.app/api?username=LXrdKnowkill&show_icons=true&theme=tokyonight&hide_border=true&bg_color=0d1117&title_color=6b7c3a&icon_color=6b7c3a" alt="GitHub Stats"/>
  <img src="https://github-readme-stats-lime-ten-54.vercel.app/api/top-langs/?username=LXrdKnowkill&layout=compact&theme=tokyonight&hide_border=true&bg_color=0d1117&title_color=6b7c3a" alt="Top Languages"/>
  <br><br>
  <img src="https://github-readme-activity-graph.vercel.app/graph?username=LXrdKnowkill&custom_title=Contribution%20Graph&hide_border=true&theme=dracula&point=6b7c3a&line=6b7c3a&text_color=f5f0e8&title_color=6b7c3a&bg_color=0d1117&area=true&area_color=6b7c3a" alt="Activity Graph"/>
</div>

---

## Research Interests

Decompilation pipeline architecture · MLIR dialect design · SSA-based variable recovery · Binary lifting and CFG recovery · Type inference in stripped binaries · Anti-analysis evasion · Dynamic instrumentation · Kernel-level reverse engineering

*Open to discussions, collaborations, and PhD opportunities in compiler infrastructure or binary analysis.*

---

## Connect

<div align="center">

[![Portfolio](https://img.shields.io/badge/Portfolio%20%26%20Blog-2d3a1f?style=for-the-badge&logo=firefox&logoColor=white)](https://lxrdknowkill.github.io/LXrdKnowkill/)
[![Email](https://img.shields.io/badge/Email-2d3a1f?style=for-the-badge&logo=gmail&logoColor=white)](mailto:Lukaskmachado@gmail.com)
[![Instagram](https://img.shields.io/badge/@patrico.istar-2d3a1f?style=for-the-badge&logo=instagram&logoColor=white)](https://instagram.com/patrico.istar)

![Discord](https://img.shields.io/badge/Discord%20%E2%80%94%20LXrd__KnowKill-2d3a1f?style=for-the-badge&logo=discord&logoColor=white)

<br>

![Profile Views](https://komarev.com/ghpvc/?username=Lxrdknowkill&color=6b7c3a&style=for-the-badge&label=PROFILE+VIEWS)

<br>

*"Code is like art, and bugs are just unexpected features."*
<br>
*— Decoding the Unknown, one dialect at a time.*

</div>

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=2d3a1f&height=120&section=footer"/>
