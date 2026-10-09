
---

### File 2: `reflection.md`

```markdown
# Learning Sprint #2: Problem 1 Reflection

## Overview & Objective
For Problem 1 of Learning Sprint #2 in SE/CprE 4210, our goal was to build an interactive educational tool to help other students understand low-level memory mechanics. We built the **Stack Buffer Overflow Explorer**, a client-side web application simulating a 32-bit x86 stack frame during string copy operations.

---

## Technical Insights & Concept Deepening

Developing this visualization deepened our understanding of stack layout and memory alignment in several key ways:

1. **Memory Directionality & Stack Growth:** While the call stack grows down toward lower addresses in x86 architectures, memory buffer writes move *upward* toward higher addresses. Visualizing memory addresses starting at `0xBFFFF000` clearly shows why unchecked buffer writes immediately threaten adjacent stack metadata—first the saved frame pointer, and the return address.

2. **The Off-by-One NUL Byte Bug:** One of the most insightful scenarios modeled was the off-by-one boundary condition. In C, null-terminated strings (`\0`) require $N+1$ bytes of storage for an $N$-character buffer. The explorer clearly demonstrates how copying an exact 8-character string into an 8-byte buffer causes the terminating null byte to spill over into the least significant byte of the saved frame pointer, showing how small software bugs can alter caller context even without direct return address overwrites.

3. **Mitigation Mechanics:** By toggling `strncpy` (bounds checking) and Stack Canaries, we observed the structural difference between **prevention** and **detection**. `strncpy` prevents the write from crossing buffer boundaries entirely. Conversely, stack canaries allow the buffer write to occur but introduce a secret guard value (`0x000D0AFF`) between the local buffer and saved frame pointer; upon function return, a canary mismatch triggers an immediate process abort (`*** stack smashing detected ***`), neutralizing control-flow hijacking before $EIP$ is loaded.

---

## AI-Assisted Workflow & Development Process

To build this application, we utilized an iterative AI-assisted development workflow:

1. **Architectural Prompting & Scope:** We defined the core domain requirements: single-file portability, responsive dark/light theme support, raw byte parsing (`\xHH`), and a byte-by-byte step slider. We prompted the AI to structure the stack frame layout using CSS Grid and standard C data structures.
2. **State Management Logic:** The core issue was synchronizing the step slider with memory arrays. The AI helped implement a `build()` and `draw()` pipeline that computes the pristine stack state (`ORIG`), applies input parsing with null-termination logic, and dynamically updates the visual DOM state.
3. **Refinement & Testing:** We tested edge cases against expected theoretical behavior, such as ensuring Little-Endian byte formatting for return address overwrites and verifying that `strcpy` stops copying upon encountering a raw `0x00` byte.

---

## Conclusion
Building this interactive explorer allowed us to get a deeper understanding of how memory works while giving us the chance to build something useful. It is always more beneficial to do something yourself because you learn more from the issues that arise.  
