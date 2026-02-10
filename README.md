C++ Game Development

//The Timber game is not finished yet, probably if i have to guess in 2/14/26 or maybe earlier it will be available to run

**From-scratch C++ game example — no external game engine.**  
Following *Beginning C++ Game Programming* by John Horton. This repository currently contains only a single study file, `timber.cpp`, implemented without a third‑party game engine. In the near future there will be added more.

---

**Engine:** **None — built from scratch**  
**Graphics library:** **SFML** used for windowing, input, and 2D rendering.

---

## Prerequisites

- **Visual Studio** with the C++ workload (recommended).  
- **SFML** matching your compiler and architecture.  
- Or **g++** (MinGW on Windows, or native g++ on Linux/macOS).

---

## Build and Run

### Visual Studio

1. Open Visual Studio and create or open a solution.  
2. Add `timber.cpp` to the project: **Right‑click Project → Add → Existing Item… → timber.cpp**.  
3. Set the project as **Startup Project**.  
4. Build the solution: **Build → Build Solution** (Ctrl+Shift+B).  
5. Run with debugger: **F5** or without debugger: **Ctrl+F5**.  
6. Copy the matching SFML DLLs from the SFML `bin` folder into the executable output folder if using dynamic libraries.


#**SFML note:** This project uses SFML for windowing and 2D rendering. Make sure you download the SFML package that matches your compiler and architecture, link the appropriate `.lib` files, and place the SFML DLLs next to the executable or on your PATH.
