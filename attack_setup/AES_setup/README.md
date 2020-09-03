# Tutorial: Building SideLine (AES) on *******

Source code is not available right now, the responsible disclosure process is still ongoing.

## Experimental Setup / Software Version

**Board**: *******  
**Processor**: *******  
**Design suite**: *******  
**SDK**: *******  

## ******* SDK

**1) Verify that the HW platform project exists in the project explorer** (if not add it)

**2) Create the attack project**
  - File -> New -> Application Project
  - Project Name -> CPU0_attack_project
  - Processor CPU0 -> *******
  - Click Next 
  - Select "Empty Application"
  - Click Finish

**3) Create the victim project**
  - File -> New -> Application Project
  - Project Name -> CPU1_victim_project
  - Processor CPU0 -> *******
  - Click Next 
  - Select "Empty Application"
  - Click Finish

You should have 5 projects

 <!---IMAGE-->


**4) Import GIT Source Code (CPU0_attack_project)**
  - First, delete the existing "src" folder in the CPU0_attack_project arborescence
  - Then, drag and drop git folders  [**src**](https://github.com/Remote-HWA/SideLine/tree/master/attack_setup/AES_setup/CPU0_attack/src) and [**inc**](https://github.com/Remote-HWA/SideLine/tree/master/attack_setup/AES_setup/CPU0_attack/inc) into CPU0_attack_project (copy files and folders)  
 Project arborescence should look like that: 
 
 <!---IMAGE-->
 
 - We need to add "inc" folder in the project include directories:
 - Right click on CPU0_attack_project -> Properties -> C/C++ General -> Paths and Symbols -> Add -> Workspace -> CPU0_attack_project/inc
 - Now all the errors should have disapeared
 
 **5) Import GIT Source Code (CPU0_victim_project)**
  - Reproduce step 4) with the CPU0_victim_project
  
Screenshot of the global arborescence: 

 <!---IMAGE-->

**6) Run Configuration**

- Connect your board in JTAG mode (PROG UART)
- Open an uart terminal (e.g. teraterm) to test the program
- Select the appropriate COM port & baud rate (115200 default or 921600 in performance mode)
- When the terminal is ready, right click CPU0_attack_project -> Run as -> Launch on hardware (System Debugger)
- Press enter in the terminal, you should see:

![teraterm1](https://user-images.githubusercontent.com/67143135/91530784-fefb1000-e90b-11ea-935a-a193831fc32c.PNG)

**7) Dual Core Configuration**

To set up the attack we need to modify the run configuration. 

- Select RUN -> Run Configurations... -> Select the saved configuration
- Select application window -> Check ps7_cortexa9_1 -> press Apply

Now victim and attack programs shouldn parralel in differents CPU cores.
- To verify, select Run
This time, CPU#0 and CPU#1 messages should appear in the console.

![teraterm2](https://user-images.githubusercontent.com/67143135/91530918-32d63580-e90c-11ea-8a3c-c0bd73b41dcc.PNG)


The attack is ready.


# Program User Manual 

### Command table
| cmd | Parameters | Description |
| --- | --- | --- |
| aes | <sample_min> <sample_max> <n_Trace> | Start AES SCA acquisition using DLL |
| dll | <n_Sample> | Print current DLL value in decimal |
  
# Save the serial output and use it for SCA

- Once the attack program is up and working, save the serial log using logging in Putty or "File->log..." in teraterm. 
- Then start the AES SCA acquisition using the command AES -> ex: aes 0 100 100000
- Once the acquisition has finished, use the python script available in [**AES_results**](https://github.com/Remote-HWA/SideLine/tree/master/attack_results/AES_results) to parse the file and conduct the CPA. Follow the guideline given in the README file associated to the script.




