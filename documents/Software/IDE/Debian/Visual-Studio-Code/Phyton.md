---
title: Python
description: 
published: true
date: 2023-12-20T06:31:37.098Z
tags: 
editor: markdown
dateCreated: 2023-12-20T05:16:16.878Z
---

# 1. Configuration
## 1.1 Install Python Extension in VS Code
- Launch VS Code.
- Go to the Extensions tab or use the shortcut (Ctrl+Shift+X).
- Search for "Python" under Microsoft category and install it.
## 1.2 Create launch.json Configuration
- Select Run from the top menu.
- Click "Add Configuration" to create launch.json.
- Choose Python configuration.

Replace the content of launch.json with the provided configuration.

     {
      "version": "0.2.0",
      "configurations": [
        {
            "name": "Python: Remote",
            "type": "python",
            "request": "attach",
            "port": 3000,
            "host": "<ip address>",
            "pathMappings": [
                {
                    "localRoot": "${workspaceFolder}",
                    "remoteRoot": "/home/user/example/Python"
                }
            ]
        }
     ]
    }
2. Remote Debugging
2.1 Connect to the RISC-V Board via SSH
Establish an SSH connection to the RISC-V board:
 $ ssh user@<ip address>  
2.2 Install debugpy
Install the debugpy library on the RISC-V board:
$ sudo pip3 install debugpy 
2.3 Start the debugpy Server
Start the debugpy server on the RISC-V board:
$ python3 -m debugpy --wait-for-client --listen 0.0.0.0:3000 executable-file.py 
2.4 Start Debugging in VS Code
Press F5 or click Run -> Start Debugging in VS Code.
Set breakpoints within VS Code.
The output will be displayed in the RISC-V board terminal and at the DEBUG CONSOLE in VS Code.