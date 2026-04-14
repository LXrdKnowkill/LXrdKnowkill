<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=ff79c6&height=140&section=header&text=Decoding%20the%20Unknown&fontSize=42&fontColor=ffffff&fontAlignY=38&desc=Binary%20Analysis%20%E2%80%A2%20Decompilation%20Research%20%E2%80%A2%20Systems%20Engineering&descSize=16&descAlignY=62"/>

<div align="center">
  <img src="https://i.imgur.com/VAkEz8u.gif" width="280">

  <br><br>

  [![Typing SVG](https://readme-typing-svg.herokuapp.com/?color=ff79c6&size=30&center=true&vCenter=true&width=1000&lines=Hello,+I'm+Yuki+%E2%9C%A8;%E2%80%94+Independent+Researcher;Founder+of+@AkashaCorporation;Building+Helix+%E2%80%94+MLIR+Decompiler;Building+HexCore+%E2%80%94+Binary+Analysis+IDE;Where+Software+Meets+Hardware+%F0%9F%94%AC)](https://git.io/typing-svg)
</div>

<br>

<div align="center">
  <h2>~ About Me ~</h2>
  <p width="650">
    I'm an <strong>independent security researcher</strong> and <strong>systems engineer</strong> from Brazil, working at the intersection of <strong>compiler infrastructure</strong> and <strong>binary analysis</strong>. My current research focuses on <strong>decompiler pipeline architecture</strong>, <strong>SSA-based variable recovery</strong>, and <strong>MLIR dialect design for reverse engineering</strong>.
  </p>
  <p width="650">
    I founded <a href="https://github.com/AkashaCorporation"><strong>@AkashaCorporation</strong></a> to build the next generation of reverse engineering tooling. My flagship project, <strong>HikariSystem HexCore</strong>, is an open-source binary analysis IDE with native engines for disassembly, emulation, and MLIR-based decompilation — battle-tested against real malware, kernel modules, and AAA game binaries.
  </p>
</div>

<br>

<div align="center">
  <h2>~ Research ~</h2>
  <br>

  <a href="#">
    <img src="https://img.shields.io/badge/📄%20Paper-Helix%3A%20MLIR%20Decompilation%20with%20Pipeline%20Loss%20Analysis-ff79c6?style=for-the-badge"/>
  </a>

  <p align="center" width="650">
    <em>"Helix: Multi-Level IR Decompilation via MLIR Dialect Lowering with Empirical Pipeline Loss Analysis"</em>
    <br><br>
    The first application of MLIR's multi-level dialect framework to binary decompilation. Through instrumented analysis of 70+ real-world functions across Linux kernel drivers, Windows PE game binaries, and CTF executables, the paper identifies that the primary decompilation quality bottleneck is at the <strong>register-to-variable recovery boundary</strong>, where a single-variable-per-register model causes cascading elimination of <strong>99.7% of recovered assignments</strong>.
    <br><br>
    Solutions: <strong>SSA variable splitting</strong> with reverse post-order traversal, <strong>Ghidra-inspired type recovery</strong>, and <strong>SCC-based irreducible CFG detection</strong>. Result: <strong>kbase_jit_allocate</strong> went from 14 lines to 133 lines (4.4% → 42.9% vs IDA Pro), with <strong>0 crashes across 70 test files</strong>.
  </p>

  <p>
    <strong>Status:</strong> Draft complete · Target venues: CC, CGO, USENIX Security
  </p>
</div>

<br>

<div align="center">
  <h2>~ Flagship Projects ~</h2>
</div>

<br>

### 🜂 HikariSystem HexCore — Binary Analysis IDE

<a href="https://github.com/LXrdKnowkill/HikariSystem-HexCore">
  <img src="https://img.shields.io/badge/🔍%20HexCore-v3.8.0--nightly-ff79c6?style=for-the-badge&logo=c%2B%2B&logoColor=white"/>
</a>

A comprehensive open-source binary analysis IDE built as a fork of code-oss, providing a unified environment for malware analysis, reverse engineering, and threat hunting. Native engines for disassembly, emulation, decompilation, and patching — all running in-process via N-API bindings without external installations.

**Battle-tested against:** ARM Mali GPU kernel driver (`mali_kbase.ko`, 45MB, 7,313 functions), Rise of the Tomb Raider (Windows PE64, AAA game engine), Riot Vanguard (anti-cheat), CTF challenge binaries, and live malware samples (`Malware HexCore Defeat.exe` v1/v2/v3 with API hashing, anti-VM, and anti-debug).

**Tech stack:** TypeScript · C++23 · MLIR · LLVM 18.1.8 · Capstone · Unicorn · Remill · Z3 · Souper · Electron · Node.js N-API

<br>

### ⚗️ Helix — MLIR-based Decompiler Engine

<a href="#">
  <img src="https://img.shields.io/badge/⚗️%20Helix-v0.9.0-9580ff?style=for-the-badge&logo=llvm&logoColor=white"/>
</a>

The decompilation engine inside HexCore. C++23/MLIR pipeline with **19 analysis passes** organized into three custom dialects: **HelixLow** (machine-level), **HelixMid** (ISA-agnostic typed SSA), and **HelixHigh** (C-level constructs). The first decompiler built on MLIR's multi-level IR framework.

**v0.9.0 highlights:**
- 70/70 test files crash-free, 100% confidence on all functions
- SSA variable splitting with RPO + immediate dominator seeding
- Ghidra-inspired type recovery (44% typed parameters, from 0%)
- SCC-based irreducible CFG detection via Tarjan's algorithm
- Variable coalescing, dynamic array detection, alias analysis, RTTI class naming
- Read-before-write initializers, depth-limited expression propagation
- Per-function confidence scoring with quality penalties and bonuses

<br>

### 🧭 Pathfinder — Pre-Lift CFG Recovery Engine

<a href="#">
  <img src="https://img.shields.io/badge/🧭%20Pathfinder-v0.2.0-50fa7b?style=for-the-badge"/>
</a>

A novel pre-lift CFG analysis engine that uses `.pdata`/`.symtab` boundaries, recursive descent disassembly, and jump table resolution to discover basic blocks and function boundaries before they reach the lifter. On `kbase_jit_allocate` (2,137 bytes), Pathfinder discovers **142 leaders from 479 instructions** — a level of pre-lift CFG visibility that no existing decompiler provides.

Architecture-aware dispatch (x86 recursive descent + x64 batch decode + ARM64 linear decode), MSVC/GCC pattern recognition for jump tables, and tail call detection via function boundary metadata.

<br>

### 🧪 hexcore-souper — First Windows N-API Build of Google Souper

<a href="#">
  <img src="https://img.shields.io/badge/🧪%20Souper-v0.2.0-bd93f9?style=for-the-badge"/>
</a>

The **first Windows N-API port of Google Souper** with Z3 SMT solving. Souper is a superoptimizer that uses constraint solving to find LLVM IR optimizations missed by traditional compilers. Until now, Souper was only available on Linux as a CLI tool — HexCore's port makes it accessible to Node.js applications on Windows for the first time.

**Empirical finding:** Near-zero impact on production binaries (kernel modules, ROTTR), but valuable for obfuscated/cryptographic analysis where superoptimization shines. Documented as a negative result — useful for the community to know.

<br>

### 🜇 Project Azoth — Clean-Room Dynamic Analysis Framework

<a href="#">
  <img src="https://img.shields.io/badge/🜇%20Azoth-In%20Development-ffb86c?style=for-the-badge"/>
</a>

A clean-room, Apache-2.0 licensed dynamic analysis framework built in **Rust + C++23**. Codenamed Project Azoth (the alchemical name for mercury — the "animating spirit" of transformation), Elixir is HexCore's next-generation emulation engine with four tiers: Unicorn-driven CPU emulation, multi-format binary loaders (PE/ELF/Mach-O), OS-level abstraction (Windows + Linux syscalls, API hooks, VFS, Registry, TEB/PEB), and Frida-style instrumentation with SharedArrayBuffer zero-copy event pipeline.

**Designed to replace Qiling and bring Frida-style dynamic instrumentation to HexCore at the emulation layer.**

<br>

<div align="center">
  <h2>~ Selected Engineering Achievements ~</h2>
</div>

| Achievement | Impact |
|-------------|--------|
| **Helix MLIR pipeline** | First decompiler built on MLIR's multi-level dialect framework |
| **SSA variable splitting** | Resolved 99.7% assignment loss in decompiler dead-code elimination |
| **Pathfinder CFG engine** | Discovered 142 leaders in 2KB of kernel code (pre-lift) |
| **First Windows Souper port** | Google Souper + Z3 accessible from Node.js on Windows |
| **SAB zero-copy IPC** | Lock-free SharedArrayBuffer ring buffer eliminating 65% TSFN drop rate |
| **HEXCORE_DEFEAT v3 emulation** | 1M instructions executed, 23,128 API calls captured against custom anti-analysis malware |
| **Pipeline loss analysis methodology** | First per-stage operation survival data for any decompilation pipeline |
| **MSVC C++ data import handling** | Solved `std::cout` vbtable access in PE emulation (nobody else has this) |

<br>

<div align="center">
  <h2>📇 ~ Technical Arsenal ~ 📇</h2>
  <br>

  <p><strong>Compiler & Systems</strong></p>
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=cpp,c,rust,go,asm,cmake&perline=6" />
  </a>
  <br><br>

  <p><strong>Binary Analysis & RE</strong></p>
  <p>
    <img src="https://img.shields.io/badge/MLIR-262577?style=for-the-badge&logo=llvm&logoColor=white"/>
    <img src="https://img.shields.io/badge/LLVM-262577?style=for-the-badge&logo=llvm&logoColor=white"/>
    <img src="https://img.shields.io/badge/Capstone-1A1A1A?style=for-the-badge"/>
    <img src="https://img.shields.io/badge/Unicorn-FFA500?style=for-the-badge"/>
    <img src="https://img.shields.io/badge/Remill-4B0082?style=for-the-badge"/>
    <img src="https://img.shields.io/badge/Z3-005571?style=for-the-badge"/>
    <img src="https://img.shields.io/badge/Souper-2E4053?style=for-the-badge"/>
  </p>
  <br>

  <p><strong>App & Web Stack</strong></p>
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=nodejs,ts,electron,tauri,react,next&perline=6" />
  </a>
  <br><br>

  <p><strong>DevOps & Tools</strong></p>
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=git,github,docker,linux,windows,vscode&perline=6" />
  </a>
</div>

<br>

<div align="center">
  <h2>~ GitHub Stats ~</h2>
  <div align="center">
    <img src="https://github-readme-stats-lime-ten-54.vercel.app/api?username=LXrdKnowkill&show_icons=true&theme=tokyonight&hide_border=true&bg_color=0d1117&title_color=ff79c6&icon_color=ff79c6" alt="Yuki's GitHub Stats"/>
    <img src="https://github-readme-stats-lime-ten-54.vercel.app/api/top-langs/?username=LXrdKnowkill&layout=compact&theme=tokyonight&hide_border=true&bg_color=0d1117&title_color=ff79c6" alt="Top Languages"/>
  </div>
  <br>
  <img src="https://github-readme-activity-graph.vercel.app/graph?username=LXrdKnowkill&custom_title=Contribution%20Graph&hide_border=true&theme=dracula&point=ff79c6&line=ff79c6&text_color=f8f8f2&title_color=ff79c6&bg_color=282a36&area=true&area_color=ff79c6" alt="Yuki's Activity Graph"/>
</div>

<br>

<div align="center">
  <h2>~ Research Interests ~</h2>
  <p>
    Decompilation pipeline architecture · MLIR dialect design · SSA-based variable recovery
    <br>
    Binary lifting and CFG recovery · Type inference in stripped binaries
    <br>
    Anti-analysis evasion · Dynamic instrumentation · Kernel-level reverse engineering
  </p>
  <p>
    <em>Open to discussions, collaborations, and PhD opportunities in compiler infrastructure or binary analysis.</em>
  </p>
</div>

<br>

<div align="center">
  <h2>~ Connect ~</h2>

  <a href="https://lxrdknowkill.github.io/LXrdKnowkill/" target="_blank">
    <img src="https://img.shields.io/badge/-Portfolio%20%26%20Blog-ff79c6?style=for-the-badge&logo=firefox&logoColor=white" alt="Portfolio Badge">
  </a>
  <a href="mailto:Lukaskmachado@gmail.com">
    <img src="https://img.shields.io/badge/-Email-ff79c6?style=for-the-badge&logo=gmail&logoColor=white" alt="Email Badge">
  </a>
  <a href="https://instagram.com/patrico.istar" target="_blank">
    <img src="https://img.shields.io/badge/-@patrico.istar-ff79c6?style=for-the-badge&logo=instagram&logoColor=white" alt="Instagram Badge">
  </a>
  <br><br>
  <img src="https://img.shields.io/badge/Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white" alt="Discord Badge"/>
  <p><b>LXrd_KnowKill</b></p>
</div>

<br>

<div align="center">
  <h2>💖 ~ Thanks for visiting ~ 💖</h2>
  <img src="https://media.tenor.com/On7KVX2S9zAAAAAi/signalis-ariane-yeong.gif" width="100">
  <br><br>
  <img src="https://komarev.com/ghpvc/?username=Lxrdknowkill&color=ff79c6&style=for-the-badge&label=PROFILE+VIEWS">
  <br><br>
  <p><em>"Code is like art, and bugs are just unexpected features."</em></p>
  <p><em>— Decoding the Unknown, one dialect at a time.</em></p>
</div>

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=ff79c6&height=120&section=footer"/>
