# Tutorial: Building SideLine (RSA) on Xilinx Zynq-7000 SoC

## Experimental Setup / Software Version

- Board: Zybo PB200-279 REV B
- Processor: Xilinx Zynq XC7Z010-1CLG400C
- Design suite: Vivado 2018.1
- SDK: Xilinx SDK 2018.1

## Prelude: Vivado

If you already have a working Hardware Platform Specification File for your board, you can skip this step and import it directly in the SDK.
For those who don't have this file, Vivado allows us to create and customize it. 

**1) Create New Vivado Project**
  - Start Vivado
  - Select "Create Project" 
  - Do not add constraint or source files
  - Select your board part (here Zybo). *If the board file does not appear in your vivado version, download it and [**add it**](https://reference.digilentinc.com/reference/software/vivado/board-files?redirect=1)*
  
**2) Create a simple block design**
  - Click on "Create Block Design" and name it "SideLine"
  - In the "Diagram" window, click on "+" to add an IP
  - Add "Zynq7 processing system" block
  - Click on "Run block automation"
  - Make sure that the "Apply Board Preset" is checked then press "OK"
  - (optional) Modify UART1 baud rate to 921600 bauds (increases attack speed)
  - Connect "M_AXI_GP0_ACLK" to "FCLK_CLK0"
  - In the "Sources" menu, right click on the block design and select "Create HDL Wrapper"
  
**3) Generate Bitstream**
 - Click on "Generate block design" located in the flow navigator
 - if successful select "Generate Bitstream" located in the flow navigator 

**4) Export HW**
- File -> Export -> Export HW (check include bitstream)
- File -> Launch SDK)

## Xilinx SDK 

**1) Verify that the HW platform project exists in the project explorer** (if not add it)

**2) Create the RSA project**
  - File -> New -> Application Project
  - Project Name -> RSA_viewer_project
  - Processor -> ps7_cortexa9_0
  - Click Next 
  - Select "Empty Application"
  - Click Finish

You should have 3 projects

<!---IMAGE-->


**3) Import GIT Source Code (RSA_setup)**
  - First, delete the existing "src" folder in the RSA_viewer_project arborescence
  - Then, drag and drop git folders [**src**](https://github.com/Remote-HWA/SideLine/tree/master/attack_setup/RSA_setup/RSA_sources/src), [**inc**](https://github.com/Remote-HWA/SideLine/tree/master/attack_setup/RSA_setup/RSA_sources/inc), wolfcrypt and wolfssl into RSA_viewer_project (copy files and folders)  
 Project arborescence should look like that: 
 
<!---IMAGE-->
 
 - We need to add "inc" folder in the project include directories:
 - Right click on RSA_viewer_project -> Properties -> C/C++ General -> Paths and Symbols -> Add -> Workspace -> RSA_viewer_project/inc
 - Now all the errors should have disapeared
 
**4) Run Configuration**

- Connect your board in JTAG mode (PROG UART)
- Open an uart terminal (e.g. teraterm) to test the program
- Select the appropriate COM port & baud rate (115200 default)
- When the terminal is ready, right click RSA_viewer_project -> Run as -> Launch on hardware (System Debugger)
- Press enter in the terminal, you should see:

![teraterm1](https://user-images.githubusercontent.com/67143135/91533438-294ecc80-e910-11ea-9cd5-e62caad463d8.PNG)


The attack is ready.

# Program User Manual 

### Command table
| cmd | Parameters | Description |
| --- | --- | --- |
| naive | <sample_min> <sample_max> <n_Trace> | Start Naive RSA SCA acquisition using DLL |
| const | <sample_min> <sample_max> <n_Trace> | Start Constant Time RSA SCA acquisition using DLL |
| ladder | <sample_min> <sample_max> <n_Trace> | Start Montgomery Ladder RSA SCA acquisition using DLL |
| dll | <n_Sample> | Print current DLL value in decimal |
  
# Save the serial output and use it for SCA

- Once the attack program is up and working, save the serial log using logging in Putty or "File->log..." in teraterm. 
- Then start the RSA SCA acquisition using the command RSA -> ex: naive 0 50000 1000
- Once the acquisition has finished, use the python script available in [**RSA_results**](https://github.com/Remote-HWA/SideLine/tree/master/attack_results/RSA_results) to parse the datafile and conduct the SPA. Follow the guidelines given in the README file associated to the script.







  



