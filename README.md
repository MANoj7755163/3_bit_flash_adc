# 3_bit_flash_adc
- [IMPLEMENTATION-OF-HIGH-SPEED-3-BIT-FLASH-TYPE-ADC](#implementation-of-high-speed-3-bit-flash-type-adc)
- [Abstract](#abstract)
- [Reference Circuit Diagram](#reference-circuit-diagram)
- [Circuit Details](#circuit-details)
- [Resolution of ADC](#resolution-of-adc)
- [Proposed Methodology](#proposed-methodology)
- [EDA Tools Used](#eda-tools-used)
- [Verilog Code](#verilog-code)
- [Makerchip](#makerchip)
- [Creating model of 8:3 Encoder using NgVeri](#creating-model-of-8-3-encoder-using-ngveri)
- [Schematics](#schematics)
- [Netlist](#netlist)
- [Output Waveforms](#output-waveforms)
- [GAW Waveforms](#gaw-waveforms)
- [Author](#author)
- [Acknowledgements](#acknowledgements)
- [References](#references)

# Abstract 
ADC is an integral component of any electronic circuit which converts continuous time continuous amplitude analog signal into continuous time discrete amplitude digital signal. Among all the types of ADCs, flash type or direct conversion ADC is considered as the high speed ADC. This paper describes the circuit implementation & simulation of flash type ADC.

# Reference Circuit Diagram
![image](https://user-images.githubusercontent.com/100668140/157507114-9d176bab-0dea-46c0-9a8f-f3aa83c42c9b.png)

# Circuit Details

A flash ADC uses linear voltage ladder with comparators at every stage which compares the input voltage with successive reference voltages which gives output in terms of 0 or 1 i.e. in digital form. Comparing with other types of ADC, flash ADC requires only single clock cycle for conversion, hence it is called as high speed ADC among all. At every resistor ladder tap, the voltages are created as 7Vref/8, 6Vref/8 upto 1Vref/8 respectively from top to bottom, connected to inverting terminal of opamp at every stage. These voltages are compared with input analog voltage and output of the opamp will be either Vsat or 0 which is represented as digital 1 & 0 respectively. These signals are provided to a 8:3 priority encoder which converts the digital data in binary format. 

# Resolution of ADC

Resolution is one of the important design constraint of any ADC. It basically indicates the smallest incremental change in input to which output can respond. In the proposed design, we are keeping Vref as 5V, hence resolution of proposed ADC design is calculated by the formula :

                             𝑅𝑒𝑠𝑜𝑙𝑢𝑡𝑖𝑜𝑛 = (𝑅𝑒𝑓𝑒𝑟𝑒𝑛𝑐𝑒 𝑉𝑜𝑙𝑡𝑎𝑔𝑒)/2^n = 5/2^3 = 5/8 = 0.625V
            
Where, n is the number of output binary bits.

# Proposed Methodology 

•	Step 1 : 		Writing Verilog code for 8:3 Priority Encoder & simulating on Makerchip

•	Step 2 : 		Model creation on NgVeri

•	Step 3 :		Schematics creation

•	Step 4 :		Creating Netlist

•	Step 5 :		Setting simulation instance parameters on KicadToNgspice converter

•	Step 6: 		Simulation & Verification of results

# EDA Tools Used

**eSim**

It is an Open Source EDA developed by FOSSEE, IIT Bombay. It is used for electronic circuit simulation. It is made by the combination of two software namely NgSpice and KiCAD. For more details refer:

https://esim.fossee.in/home

**NgSpice**

It is an Open Source Software for Spice Simulations. For more details refer:

http://ngspice.sourceforge.net/docs.html

**Makerchip**

It is an Online Web Browser IDE for Verilog/System-verilog/TL-Verilog Simulation. For more details refer:

https://www.makerchip.com/

**Verilator**

It is a tool which converts Verilog code to C++ objects. For more details refer:

https://www.veripool.org/verilator/


# Verilog Code

                     `timescale 1ns / 1ps
                      //////////////////////////////////////////////////////////////////////////////////
                     // Company: 
                     // Engineer: 
                     // 
                    // Create Date: 05.03.2022 15:30:05
                    // Design Name: 
                   // Module Name: priority_encoder
                  // Project Name: 
                  // Target Devices: 
                 // Tool Versions: 
                 // Description: 
                 // 
                 // Dependencies: 
                 // 
                 // Revision:
                // Revision 0.01 - File Created
               // Additional Comments:
               // 
                 //////////////////////////////////////////////////////////////////////////////////



                module priority_encoder(din,dout);
                input[7:0]din;
                output reg[2:0]dout;
  
               always@(din)
                 begin
              casex(din)
                 8'b00000001 :dout = 3'b000;
                 8'b0000001X :dout = 3'b001;
                 8'b000001XX :dout = 3'b010;
                 8'b00001XXX :dout = 3'b011;
                 8'b0001XXXX :dout = 3'b100;
                 8'b001XXXXX :dout = 3'b101;
                 8'b01XXXXXX :dout = 3'b110;
                 8'b1XXXXXXX :dout = 3'b111;
                  endcase

      
     
      
                 end
                 endmodule

# Makerchip 

 
            \TLV_version 1d: tl-x.org
            \SV
            /* verilator lint_off UNUSED*/  /* verilator lint_off DECLFILENAME*/  /* verilator lint_off BLKSEQ*/  /* verilator lint_off WIDTH*/  /* verilator lint_off SELRANGE*/             /* verilator lint_off PINCONNECTEMPTY*/  /* verilator lint_off DEFPARAM*/  /* verilator lint_off IMPLICIT*/  /* verilator lint_off COMBDLY*/  /* verilator lint_off               SYNCASYNCNET*/  /* verilator lint_off UNOPTFLAT */  /* verilator lint_off UNSIGNED*/  /* verilator lint_off CASEINCOMPLETE*/  /* verilator lint_off UNDRIVEN*/  /*               verilator lint_off VARHIDDEN*/  /* verilator lint_off CASEX*/  /* verilator lint_off CASEOVERLAP*/  /* verilator lint_off PINMISSING*/  /* verilator lint_off LATCH*/            /* verilator lint_off BLKANDNBLK*/  /* verilator lint_off MULTIDRIVEN*/  /* verilator lint_off NULLPORT*/  /* verilator lint_off EOFNEWLINE*/  /* verilator lint_off              WIDTHCONCAT*/  /* verilator lint_off ASSIGNDLY*/  /* verilator lint_off MODDUP*/  /* verilator lint_off STMTDLY*/  /* verilator lint_off LITENDIAN*/  /* verilator                lint_off INITIALDLY*/  /* verilator lint_off */  

          //Your Verilog/System Verilog Code Starts Here:
          `timescale 1ns / 1ps
          //////////////////////////////////////////////////////////////////////////////////
          // Company: 
         // Engineer: 
         // 
         // Create Date: 05.03.2022 15:30:05
        // Design Name: 
        // Module Name: priority_encoder
        // Project Name: 
       // Target Devices: 
       // Tool Versions: 
      // Description: 
      // 
     // Dependencies: 
     // 
    // Revision:
    // Revision 0.01 - File Created
    // Additional Comments:
    // 
    //////////////////////////////////////////////////////////////////////////////////



    module priority_encoder(din,dout);
    input[7:0]din;
    output reg[2:0]dout;
  
    always@(din)
    begin
      casex(din)
         8'b00000001 :dout = 3'b000;
         8'b0000001X :dout = 3'b001;
         8'b000001XX :dout = 3'b010;
         8'b00001XXX :dout = 3'b011;
         8'b0001XXXX :dout = 3'b100;
         8'b001XXXXX :dout = 3'b101;
         8'b01XXXXXX :dout = 3'b110;
         8'b1XXXXXXX :dout = 3'b111;
         endcase

      
     
      
         end
         endmodule

 


        //Top Module Code Starts here:
	      module top(input logic clk, input logic reset, input logic [31:0] cyc_cnt, output logic passed, output logic failed);
		    logic  [7:0] din;//input
		    logic reg [2:0] dout;//output
        //The $random() can be replaced if user wants to assign values
		    assign din = $random();
		    priority_encoder priority_encoder(.din(din), .dout(dout));
	
       \TLV
        //Add \TLV here if desired                                     
       \SV
       endmodule

Following are the several waveforms for different inputs given to 8:3 encoder & their respective outputs :
![Capture1](https://user-images.githubusercontent.com/100668140/157508988-ca580f43-fb80-4836-bcfc-0725d0e078cd.PNG)

# Schematics

![Capture6](https://user-images.githubusercontent.com/100668140/157518064-cd1052ce-02f7-403b-9bff-930aa8c550c5.PNG)

![Capture2](https://user-images.githubusercontent.com/100668140/157518225-3adac47e-9d64-4d2d-873f-465b9bbf6abe.PNG)
![Capture3](https://user-images.githubusercontent.com/100668140/157518296-ea8e1444-ebc6-44f9-a0b9-e0efde8bd2c3.PNG)
![Capture5](https://user-images.githubusercontent.com/100668140/157518427-05054595-41b9-470f-8cd6-20d66851a0c5.PNG)





