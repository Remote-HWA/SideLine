# Building the Attack on Xilinx Zynq-7000


## Experimental Setup 

Zybo PB200-279 REV-B
Zynq XC7Z010CLG400

MASTER DLL ADDR: 0xF80061E0

## VIVADO

1) Create New Vivado Project
  - Select your board (Here Zybo)
  - No constraint file
  - No source file
2) Create a simple block design
  - Add "Zynq7 processing system"
  - Run block automation
  - Check apply board preset then press "OK"
  - (optional) Modify UART1 baud rate to 921600 bauds (increases attack speed)
  - Connect "M_AXI_GP0_ACLK" to "FCLK_CLK0"
  - Create HDL wrapper
3) Generate Block Design (Global)
4) Generate Bitstream
5) Export HW
- File -> Export -> Export HW (check include bitstream)
- File -> Launch SDK

## XILINX SDK (VITIS)

1) Verify that the HW platform project exists in the project explorer 

2) Create the attack project
  - File -> New -> Application Project
  - Project Name -> CPU0_attack_project
  - Processor CPU0 -> ps7_cortexa9_0
  - Click Next 
  - Select "Empty Application"
  - Click Finish

3) Create the victim project
  - File -> New -> Application Project
  - Project Name -> CPU1_victim_project
  - Processor CPU0 -> ps7_cortexa9_1
  - Click Next 
  - Select "Empty Application"
  - Click Finish

You should have 5 projects

4) Import Source Code (CPU0_attack_project)
  - Delete src folder in the CPU0_attack_project arborescence
  - Copy & paste git folders  "SideLine/attack_script/CPU0/src" and "SideLine/attack_script/CPU0/inc" into CPU0_attack_project (copy files and folders)  
 Project arborescence should look like that: 
 
 Picture
 
 - We need to add "inc" folder in the project include directories:
 - Right click on CPU0_attack_project -> Properties -> C/C++ General -> Paths and Symbols -> Add -> Workspace -> CPU0_attack_project/inc
 - Now all the errors should have disapeared
 
 5) Import Source Code (CPU0_victim_project)
  - Reproduce step 4) with the CPU0_victim_project
  
Screenshot of the global arborescence: 

PHOTO


6) Run Configuration

- Connect your board in JTAG mode (PROG UART)
- Right click CPU0_attack_project -> Run as -> Launch on hardware (System Debugger)
- Open SDK terminal to test the console -> click on "plus" icon 
- Select the appropriate COM port & baud rate (115200 default) -> press OK
- Press enter in the shell. you should see:


PHOTO

7) Dual Core Configuration

To set up the attack we need to modify the run configuration. 

- Select RUN -> Run Configurations... -> Select the saved configuration
- Select application window -> Check ps7_cortexa9_1 -> press Apply

Now victim and attack programs shouldn parralel in differents CPU cores.
- To verify, select Run
Messages from the CPU0 and the CPU12 should appear in the console.

PHOTO

The attack is ready.









  



