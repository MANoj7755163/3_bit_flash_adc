# 3_bit_flash_adc
- [Abstract](#abstract)
- [Reference Circuit Diagram](#reference-circuit-diagram)
- [Circuit Details](#circuit-details)
- [Resolution of ADC](#resolution-of-adc)
- [Proposed Methodology](#proposed-methodology)
- [EDA Tools Used](#eda-tools-used)
- [Verilog Code](#verilog-code)
- [Makerchip](#makerchip)
- [Creating model of 8:3 Encoder using NgVeri](#creating-model-of-8-3-encoder-using-ngveri)
- [Schematic](#schematic)
- [Output Waveforms](#output-waveforms)
- [Author](#author)
- [Acknowledgements](#acknowledgements)
- [References](#references)

# Abstract 
Analog to Digital converters are 
essential in all communication and signal 
processing applications. Among all ADC’S 
Flash ADC has a high speed conversion rate. It 
has a capacity of sampling a signal up to Giga 
Bites. The conventional Flash ADC contains
the resistor ladder network, comparator, and 
encoder. Due to the use of resistor ladder 
network in conventional Flash ADC static 
power consumption is more to overcome this 
issue, new 3-Bit Flash ADC has been proposed. 
The proposed ADC is consists of sample and 
hold (S/H) circuit, threshold modified 
comparator circuit and priority encoder. The 
design is implemented with a supply voltage 
of 1.8 V and clock frequency of 1M Hz. 

# Reference Circuit Diagram
![image](https://user-images.githubusercontent.com/100668140/157507114-9d176bab-0dea-46c0-9a8f-f3aa83c42c9b.png)

# Circuit Details

figure shown a 3 bit flash type A/D converter 
which requires (2^3-1)=8 comparators.The 
analog input which is to be converted is 
connected to the non-inverting terminal.Input 
terminal of comparator where as the inverting 
input terminals of op-ams are connected to a 
set of reference voltage provided by voltage 
divider that divides it into 7 equal increment 
levels.
Each level is compared to the analog input by 
a voltage comparator.All comparators O/Ps 
are connected to a priority encoder,which 
produces a digital o/p corresponding to the 
i/p having highest priority.Thus,the digital o/p 
represents the voltage that is closest in value 
to the analog input



# Resolution of ADC

Resolution is one of the important design constraint of any ADC. It basically indicates the smallest incremental change in input to which output can respond. In the proposed design, we are keeping Vref as 5V, hence resolution of proposed ADC design is calculated by the formula :

                             𝑅𝑒𝑠𝑜𝑙𝑢𝑡𝑖𝑜𝑛 = (𝑅𝑒𝑓𝑒𝑟𝑒𝑛𝑐𝑒 𝑉𝑜𝑙𝑡𝑎𝑔𝑒)/2^n = 5/2^3 = 5/8 = 0.625V
            
Where, n is the number of output binary bits.

# Proposed Methodology 

• Writing Verilog code for 8:3 Priority Encoder & simulating on Makerchip

• Model creation on NgVeri

• Schematics creation

• Creating Netlist

• Setting simulation instance parameters on KicadToNgspice converter

• Simulation & Verification of results

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

# Schematic

![Capture6](https://user-images.githubusercontent.com/100668140/157518064-cd1052ce-02f7-403b-9bff-930aa8c550c5.PNG)

![Capture2](https://user-images.githubusercontent.com/100668140/157518225-3adac47e-9d64-4d2d-873f-465b9bbf6abe.PNG)
![Capture3](https://user-images.githubusercontent.com/100668140/157518296-ea8e1444-ebc6-44f9-a0b9-e0efde8bd2c3.PNG)
![Capture5](https://user-images.githubusercontent.com/100668140/157518427-05054595-41b9-470f-8cd6-20d66851a0c5.PNG)

# Output Waveforms

For output testing I have taken Vref as 5v and Va as 5v. Also positive supply is 5v. So, voltages at inverting terminal of all the comparators are less than the inverting terminal voltage(i.e 5V) due to voltage divider circuit. So, output of all 7 comparators will be logic high (5v). Hence all the output digital bit will  be high(logic-1 i.e 5)

![manoj2](https://user-images.githubusercontent.com/100668140/157723827-3bf394af-e0af-40aa-8ec5-02b8e55c90fb.JPG)


![manoj](https://user-images.githubusercontent.com/100668140/157721278-0e1d16c0-88e6-4062-8686-9005f2e7f273.JPG)

# Author

MANOJ KUMAR SINGH

M.Tech 2nd semester

Indian Institute Of Information Technology,Allahabad


# Acknowledgements

1.	Kunal Ghosh (Co-Founder, VLSI System Design Pvt. Ltd.)

2.	FOSSEE, IIT Bombay	

3.	Steve Hoover (Founder, Redwood EDA)
	
4.	Sumanto Kar (eSim Team, FOSSEE, IIT Bombay)

# References

1.	 . Swarupa B N, Dr. Vijaya Prakash A M, 
Kumaraswamy K V “Implementation of a 3-bit 
Flash ADC using TIQ Modified Comparator 
Circuit and NORROM based Encoder” 
International Journal of Innovative Research 
in Computer and Communication Engineering 
Vol. 5, Issue 5, May 2016. 

2.	Mayur. S. M, Siddharth R. K, Nithin Kumar 
Y. B, Vasantha M. H “Design of Low Power 5-
bit Hybrid Flash ADC” 2016 IEEE Computer 
Society Annual Symposium on VLSI







