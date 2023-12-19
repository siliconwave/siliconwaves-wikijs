---
title: Steps to Bring up Node js Server Debugging Using VS Code
description: 
published: true
date: 2023-12-19T11:18:32.072Z
tags: 
editor: markdown
dateCreated: 2023-12-19T11:18:32.072Z
---


1. Create launch.json Configuration:
    - Select `Run` from the top menu.
    - Click "Add Configuration" to create launch.json.
    - Choose `Node.js: Attach` configuration.
    - Overwrite the content of launch.json with the following:
    {
        "version":"0.2.0",
        "configurations":[
            {
                "name":"Node: Remote",
                "type":"node",
                "request":"attach",
                "port":2000,
                "address":"<ip-address>",
                "localRoot":"${workspaceFolder}",
                "remoteRoot":"<path to Node js directory>"
            }
        ]
    }
    - Updated the `remoteRoot` with the path of Node JS file on the board
1. Connect to the RISC-V board via SSH:
    $ ssh root@<ip-address>
1. Write a simple `add.js` Program:
    1. Create a simple `add.js` node js program on RISC V alone.
    const num1 = 5;
    const num2 = 10;
    const sum = num1 + num2;
    console.log(`The sum of ${num1} and ${num2} is ${sum}`);
    console.log('END');
1. Start the Node js server:
    $ node --inspect-brk=0.0.0.0:4000 add.js
        (Ensure the port number matches the one in the launch.json configuration)
    1. Start Debugging in VS Code:
    - Press F5 or click Run -> Start Debugging.
    - The breakpoints will be set in VS Code.
    - The output will be shown in the RISC-V board terminal and `DEBUG CONSOLE` in vs code.

You can now remotely debug your RISC-V code using VS Code. sure the IP address, port, and ‘remoteRoot’ are correctly configured based on your setup.