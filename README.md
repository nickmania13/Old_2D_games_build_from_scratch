C++ Game Development

**From-scratch C++ game example — no external game engine.**  
Following *Beginning C++ Game Programming* by John Horton. This repository currently contains only a single study file, `timber.cpp`, implemented without a third‑party game engine. In the near future there will be added more.

---

## What this repo is
A personal study example implementing concepts from *Beginning C++ Game Programming* by John Horton. The code is written from scratch in C++ and is intended for learning and experimentation.

---

## Files
- **`timber.cpp`** — single C++ source file containing the chapter/example code.

---

## Prerequisites
- **Visual Studio** with the C++ workload (recommended), or  
- **g++** (MinGW on Windows, or native g++ on Linux/macOS).

---

## Build and Run

### Visual Studio
1. Open Visual Studio and create a new empty project or open an existing solution.  
2. Add `timber.cpp` to the project: **Right‑click Project → Add → Existing Item… → timber.cpp**.  
3. Set the project as **Startup Project**.  
4. Build: **Build → Build Solution** (Ctrl+Shift+B).  
5. Run with debugger: **F5** or without debugger: **Ctrl+F5**.  
6. The executable will be in the project output folder (for example `.\Debug\` or `.\Release\`).

### Command line with MSVC
rem --- set your paths here ---
set TIMBER_DIR=C:\path\to\folder\containing\timber.cpp
set SFML_DIR=C:\path\to\SFML

rem --- go to source folder ---
cd /d "%TIMBER_DIR%"

rem --- compile and link (Release, dynamic SFML libs) ---
cl /EHsc timber.cpp /I"%SFML_DIR%\include" /link /LIBPATH:"%SFML_DIR%\lib\x86" sfml-graphics.lib sfml-window.lib sfml-system.lib /OUT:timber.exe

rem --- copy matching SFML DLLs next to the exe ---
copy "%SFML_DIR%\bin\x86\*.dll" .

rem --- run the program ---
timber.exe

#**SFML note:** This project uses SFML for windowing and 2D rendering. Make sure you download the SFML package that matches your compiler and architecture, link the appropriate `.lib` files, and place the SFML DLLs next to the executable or on your PATH.
