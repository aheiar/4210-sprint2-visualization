# Stack Buffer Overflow Explorer

An interactive, browser-based educational visualization designed for **SE/CprE 4210: Software Security (Learning Sprint #2)** at Iowa State University. 

This application provides a visual and intuitive model of a 32-bit C stack frame during string copy operations (`strcpy` vs `strncpy`). It allows students to observe step-by-step how memory bounds violations corrupt adjacent stack data—such as the saved frame pointer (EBP) and return address (EIP)—and how mitigations like stack canaries detect stack smashing.

---

## Features

- **Interactive Controls:**
  - **Custom String Input:** Test arbitrary strings or raw byte values (using hex format, e.g., `\x78\x56\x34\x12`).
  - **Buffer Sizing:** Dynamically resize the buffer from 8 to 16 bytes.
  - **Defensive Toggles:** Enable `strncpy` bounded copying or toggle Stack Canaries on/off.
  - **Copy Progress Slider:** Step through `strcpy` byte-by-byte to see exactly when and where stack boundaries are crossed.
  - **Preset Scenarios:** One-click buttons to simulate normal execution, off-by-one NUL byte errors, frame pointer corruption, return address smashing, and address injection.

- **Stack Frame Grid:**
  - Visual representation of memory starting from `0xBFFFF000`.
  - Color-coded memory segments for the target buffer, stack canary, saved frame pointer, and return address.
  - Highlights modified bytes in red (`.hit`) to illustrate state changes instantly.

- **Real-Time Analysis & Verdict:**
  - Live feedback banner describing the safety state (Safe, Off-by-one, Canary corrupted/abort, Return address overwritten / Control-flow hijack).

---

## How to Run

No server or external dependencies are required.

1. Download or clone this repository:
   ```bash
   git clone [https://github.com/YOUR_USERNAME/cpre4210-sprint2-visualization.git](https://github.com/YOUR_USERNAME/cpre4210-sprint2-visualization.git)
