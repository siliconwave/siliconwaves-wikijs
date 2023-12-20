---
title: C/C++
description: 
published: true
date: 2023-12-20T06:51:03.818Z
tags: 
editor: markdown
dateCreated: 2023-12-20T06:09:47.356Z
---

# 1. Installation Steps
## 1.1. Install gdbgui on RISC-V Board
Install the necessary dependencies and gdbgui:

    sudo apt−get install gdb python3
    sudo pip install gdbgui
## 1.2. Compile the Program
Compile the program with debugging information using −g flag:

    gcc −g <file name>.c −o <file name>
## 1.3. Start gdbgui
Run the following command in terminal to start gdbgui:

    gdbgui −r <file name>
- This will start the service at the host IP, typically http://<ip address>:5000.
- Open a web browser on your local machine and enter the URL to access gdbgui, where the respective program will gets loaded.
# 2. Debugging with gdbgui
## 2.1.Set Breakpoints and Start Debugging:
- Click on the line number in the code editor where you want to set a breakpoint.
- After placing the required breakpoint, start the program by typing r or run command in the gdb terminal. This will start the debugged program.
- Use the buttons on the top right corner of the gdbgui interface to navigate through the program's execution step-by-step, such as continue, pause, restart, step over, etc.
## 2.2. Additional Features in gdbgui:
- You can check the disassembly of code by clicking on the top menu bar and by selecting Fetch Disassembly. This allows you to debug at the assembly level.
- gdbgui allows you to track local variables, memory, expressions, and registers in the right panel.