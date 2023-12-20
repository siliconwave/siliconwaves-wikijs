---
title: C/C++
description: 
published: true
date: 2023-12-20T06:23:29.864Z
tags: 
editor: markdown
dateCreated: 2023-12-20T06:05:24.926Z
---

# 1. Configuration
## 1.1 Install C/C++ Debug Extension in VS Code
- Launch VS Code.
- Go to the Extensions tab or use the shortcut (Ctrl+Shift+X).
- Search for "C/C++" under Microsoft category and install it.
## 1.2 Create launch.json Configuration
- Select Run from the top menu.
- Click on "Add Configuration" to create launch.json.
- Choose C/C++: (gdb) Launch configuration.
- Replace the content of launch.json with the provided configuration.

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
            "miDebuggerPath": "/opt/riscv/bin/riscv64-unknown-linux-gnu-gdb",
            "miDebuggerServerAddress": "<ip address>:2000"
        }
       ]
      }
## 1.3 Cross Compilation Using tasks.json
- Select Terminal -> Configure Tasks.
- Create a new tasks.json file from the template.
- Replace the content of tasks.json with the provided configuration.

      {
      "version": "2.0.0",
       "tasks": [
       {
      "label": "C: Build",
      "type": "shell",
      "command": "/opt/riscv/bin/riscv64-unknown-linux-gnu-gcc",
      "args": [
        "-g",
        "${file}",
        "-o",
        "${fileDirname}/${fileBasenameNoExtension}"
      ],
      "group": {
        "kind": "build"
         }
        }
       ]
      }
# 2. Building and Remote Debugging
## 2.1 Build and Copy Executable to RISC-V Board
- Build the project by pressing Ctrl+Shift+B or by clicking Terminal --> Run Build Task.
- The binary file will be generated in the same directory as the source file.
- Copy the executable file to the RISC-V board using SCP.

      scp executable-file user@<ip address>:~/.  
## 2.2 Start GDB Server on RISC-V Board
- Connect to the RISC-V board via SSH.

      ssh user@<ip address> 
- Start the GDB server using the provided command.

      gdbserver localhost:2000 executable-file 
## 2.3 Start Debugging in VS Code
- Press F5 or click Run -> Start Debugging.
- Set breakpoints in VS Code.
- The output will be displayed in the RISC-V board terminal.
## 2.4 Check Disassembly
Right-click to view the disassembly of the code using the "Open Disassembly View" option in the VS Code editor.