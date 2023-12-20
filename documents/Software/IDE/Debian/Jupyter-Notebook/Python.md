---
title: Python
description: 
published: true
date: 2023-12-20T06:43:03.473Z
tags: 
editor: markdown
dateCreated: 2023-12-20T05:19:55.495Z
---

# 1. Installation
## 1.1 Switch to Super User Mode
     sudo su 
## 1.2 Install rustc and cargo
Download the rustup-init script and grant execute permissions:

     wget −O rustup−init.sh https://sh.rustup.rs
     chmod +x rustup−init.sh
     ./rustup−init.sh
Update the shell environment to include Cargo:

     source "$HOME/.cargo/env" 
## 1.3 Check Rustc and Cargo Version
    rustc −−version
    cargo −−version
## 1.4 Install Jupyter Notebook Using pip
    sudo pip install notebook 
# 2. Running Jupyter Notebook
## 2.1 Start Jupyter Notebook
    jupyter notebook --ip 0.0.0.0 --allow-root 
## 2.2 Access Jupyter Notebook from Host Machine
After starting Jupyter Notebook, a listening URL will be displayed.
You can access it from your host machine by changing the URL IP to the RISC-V board's IP.
# 3. Debugging
## 3.1 Launching Debugger in JupyterLab
- Access JupyterLab by clicking on the JupyterLab link in the top right corner.
- Click on the debugger icon to activate the debugger mode.
## 3.2 Setting Breakpoints
Place breakpoints by clicking on the left side of line numbers in a Python cell.
## 3.3 Executing the Program
- Click on the run icon located on the status bar to execute the program.
- The program will pause at the breakpoint.
## 3.4 Debugging Tools
A panel on the right provides debugging tools for tracking variables, call stacks, breakpoints, and source code.