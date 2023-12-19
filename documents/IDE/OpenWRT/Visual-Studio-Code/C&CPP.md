---
title: C/C++
description: 
published: true
date: 2023-12-19T13:06:03.989Z
tags: 
editor: markdown
dateCreated: 2023-12-19T13:04:00.152Z
---

# Steps to Bring up C/C++ Server Debugging Using VS Code
## 1. Install C/C++ Debug Extension in VS Code:
  - Open VS Code.
  - Go to the Extensions tab or (Ctrl+Shift+X).
  - Search for “C/C++" by Microsoft and install it.
## 2. Create launch.json Configuration:
  - Select `Run` from the top menu.
  - Click "Add Configuration" to create launch.json.
  - Choose `C/C++: (gdb) Lunch` configuration.
  - Overwrite the content of launch.json with the following:

         {
           "version": "0.2.0",
           "configurations": [
          {
          "name": "C/C++: Remote",
          "type": "cppdbg",
          "request": "launch",
          "program": "${workspaceFolder}/${fileBasenameNoExtension}",
          "cwd": "${workspaceFolder}",
          "stopAtEntry": true,
          "MIMode": "gdb",
          "miDebuggerPath": "riscv64-openwrt-linux-gdb",
          "miDebuggerServerAddress": "192.168.4.26:2000"
          }
         ]
        }
## 3. Cross Compilation Using tasks.json:
  - Select Terminal -> Configure Tasks.
  - Click `Create tasks.json file from template`.
  - Choose `Others` -> `Empty tasks.json` to create a new tasks.json file.
  - Replace the content of tasks.json with the following: 
    
         {
        "version": "2.0.0",
        "tasks": [
          {
            "label": "C: Build",
            "type": "shell",
            "command": "riscv64-openwrt-linux-gcc",
            "args": ["-g", "${file}", "-o", "${fileDirname}/${fileBasenameNoExtension}"],
            "group": {
              "kind": "build"
            }
          },
          {
            "label": "C++: Build",
            "type": "shell",
            "command": "riscv64-openwrt-linux-g++",
            "args": ["-g", "${file}", "-o", "${fileDirname}/${fileBasenameNoExtension}"],
            "group": {
              "kind": "build"
            }
           }
         ]
        }
## 4. Build and Copy Executable to RISC-V Board:
  - Press `Ctrl+Shift+B` or Click Terminal -> `Run Build Task`.
  - The binary file will be generated in the same directory as the source file.
  - Copy the executable to the RISC-V board using SCP:

        scp executable-file root@<ip address>:~/.
## 5. Start GDB Server on RISC-V Board:
 - Connect to the RISC-V board via SSH:

       ssh root@<ip address>
 - Start the GDB server:

       gdbserver localhost:2000 executable-file

   (Ensure the port number matches the one in the launch.json configuration)
## 6. Start Debugging in VS Code:
   - Press F5 or click Run -> Start Debugging.
   - The breakpoints will be set in VS Code.
   - The output will be shown in the RISC-V board terminal.
## 7. Check Disassembly :
   - To view the disassembly of the code, right-click and select `Open Disassembly View` in the VS Code editor.
   - This allows you to analyze the low-level instructions executed by the RISC-V processor.

You can now remotely debug your RISC-V code using VS Code. Make sure the IP address, port, and paths are correctly configured based on your setup.
