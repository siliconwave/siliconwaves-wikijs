---
title: Python
description: 
published: true
date: 2023-12-19T13:01:13.168Z
tags: 
editor: markdown
dateCreated: 2023-12-19T12:57:08.551Z
---


## 1. Install python and pip
     opkg update 
     opkg install python3 python3-pip
## 2. Install Python Extension in VS Code:
 - Open VS Code.
 - Go to the Extensions tab or (Ctrl+Shift+X).
 - Search for `Python` by Microsoft and install it.
## 3. Create launch.json Configuration:
- Select `Run` from the top menu.
- Click "Add Configuration" to create launch.json.
- Choose `Python` configuration.
- Overwrite the content of launch.json with the following:

        {
      "version": "0.2.0",
      "configurations": [
         {
          "name": "Python: Remote",
          "type": "python",
          "request": "attach",
          "port": 2000,
          "host": "<ip address>",
          "pathMappings": [
            {
              "localRoot": "${workspaceFolder}",
              "remoteRoot": "<path to your python file on board>"
            }
          ]
        }
       ]
      }
## 4. Connect to the RISC-V board via SSH:
     ssh user@<ip address>
## 5. Install `debugpy` :
     sudo pip3 install debugpy
## 6. Write a simple `add.py` Program:
  1. Create a simple `add.py` Python program. 
  2. The program is present on both your RISC V board and your local machine.

    n = 10
    num1 = 0
    num2 = 1
    next_number = num2
    count = 1
    while count <= n:
        print(next_number, end=" ")
        print()
        count += 1
        num1, num2 = num2, next_number
        next_number = num1 + num2
    print()
## 7. Update the firewall for port 2000:
     uci add firewall rule
     uci set firewall.@rule[-1].name='Allow GDB Server'
     uci set firewall.@rule[-1].src='*'
     uci set firewall.@rule[-1].proto='tcp'
     uci set firewall.@rule[-1].dest_port='2000'
     uci set firewall.@rule[-1].target='ACCEPT'
     uci commit firewal
## 8. Start the debugpy server:
     python3 -m debugpy --wait-for-client --listen 0.0.0.0:2000 add.py
  (Ensure the port number matches the one in the launch.json configuration)
## 9. Start Debugging in VS Code:
  - Press F5 or click Run -> Start Debugging.
  - The breakpoints will be set in VS Code.
  - The output will be shown in the RISC-V board terminal and `DEBUG CONSOLE` in vs code.

You can now remotely debug your RISC-V code using VS Code. Make sure the IP address, port, and remoteRoot are correctly configured based on your setup.
