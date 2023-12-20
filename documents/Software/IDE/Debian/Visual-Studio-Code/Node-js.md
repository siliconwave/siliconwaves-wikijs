---
title: Node.js
description: 
published: true
date: 2023-12-20T06:32:38.930Z
tags: 
editor: markdown
dateCreated: 2023-12-20T05:18:33.594Z
---

# 1. Configuration
## 1.1 Create launch.json Configuration
- Select Run from the top menu.
- Click "Add Configuration" to create launch.json.
- Choose Node.js: Attach configuration.

Replace the content of launch.json with the provided configuration.

      {
       "version": "0.2.0",
       "configurations": [
        {
            "name": "Node: Remote",
            "type": "node",
            "request": "attach",
            "port": 4000,
            "address": "192.168.4.26",
            "localRoot": "${workspaceFolder}",
            "remoteRoot": "/home/user/example/Node"
        }
       ]
      }
Update the remoteRoot path with the appropriate Node.js file path on the board.
# 2. Remote Debugging
## 2.1 Connect to the RISC-V Board
- Connect to the RISC-V board via SSH using the provided command.

      ssh user@<ip address> 
## 2.2 Start the Node.js Server
- Start the Node.js server using the provided command.
- The --inspect-brk flag enables debugging.

      node --inspect-brk=0.0.0.0:4000 executable-file.js 
## 2.3 Start Debugging in VS Code
- Press F5 or click Run -> Start Debugging.
- Set breakpoints in VS Code.

Observe the output in RISC-V board terminal and DEBUG CONSOLE in VS Code.