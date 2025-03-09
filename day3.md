###   Digital Logic with TL-Veriog with Makerchip IDE
### Makerchip IDE :
Makerchip IDE is a cloud-based integrated development environment designed for TL-Verilog and open-source hardware design. It provides a seamless platform for designing, simulating, and verifying digital circuits without requiring local installations. With built-in support for TL-Verilog, it simplifies hardware description by reducing complexity compared to traditional Verilog. Makerchip features real-time simulation, interactive waveform visualization, and debugging capabilities using Verilator, a high-performance open-source simulator. It also supports RISC-V development, allowing users to design and verify RISC-V cores efficiently. The IDE integrates with GitHub for version control and enables multi-user collaboration, making it suitable for team-based projects. With in-browser editing, syntax highlighting, and automatic RTL generation, it enhances productivity while maintaining design flexibility. Makerchip is widely used in education, research, and open-source hardware development, making it a valuable tool for learning and experimenting with digital design concepts.

### TL-Verilog and Its Features
TL-Verilog (Transaction-Level Verilog) is an extension of Verilog that simplifies hardware description by introducing transaction-level modeling (TLM). It enhances modularity, reduces repetitive coding, and improves design efficiency, making it ideal for modern digital circuit design, especially in open-source environments.

TL-Verilog eliminates the complexity of traditional Verilog by using pipelines, transactions, and implied clocking, reducing the need for explicit clock and reset logic. It is particularly useful in RISC-V core development and integrates well with cloud-based tools like Makerchip IDE.

Key Features of TL-Verilog:
#### 1. Transaction-Level Modeling (TLM):
    
- Uses transactions to abstract operations, reducing RTL complexity.
        
- Enhances reusability and modularity in circuit design. 
        
#### 2. Pipeline-Centric Approach:
    
- Simplifies pipeline design with automatic pipeline management.
        
- Reduces pipeline bugs and increases design clarity.
        
#### 3. Implied Clocking:
    
- No need for explicit clock and reset logic.
        
- The clock is inferred from the pipeline stage itself. 
        
#### 4. Concise and Readable Code:
    
- Eliminates redundant Verilog constructs.
        
- Uses compact syntax to define logic with minimal effort.
        
#### 5. Integrated with Open-Source Tools:
    
- Works seamlessly with Makerchip IDE and Verilator for simulation. 
        
- Supports open-source development, making it accessible to students and professionals. 
        
#### 6. Hierarchical and Modular Design:
    
- Encourages structured coding with reusable blocks. 
        
- Enables efficient debugging and design modification. 
        
####  7. Better Hardware Development Productivity:
    
- Reduces development time by automating repetitive tasks. 
        
- Ensures faster verification and debugging with built-in simulation tools

## LABS:
### combinational circuits implementation

#### 1. Implemenation of 2:1 mux:
 
**code**
```tlv
\m5_TLV_version 1d: tl-x.org
\m5
   
\SV
   m5_makerchip_module   
\TLV 
   $out = $sel ? $in1 :$in2;
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```
**markchip ide link** [mux2:1]( https://www.makerchip.com/sandbox/0W6fjhnMo/0Nxh0Mm)

**image**

#### 2. Multiplexer with vectors

**code**
```tlv
\m5_TLV_version 1d: tl-x.org
\m5
\SV
   m5_makerchip_module   
\TLV
   $out = $sel ? $in1[7:0] : $in2[7:0];
   
   /.
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```
**makerchip ide link:** [mux_with_vectors](https://www.makerchip.com/sandbox/0W6fjhnMo/0r0h8DL)
**image**

#### Multiplexer 4:1
**code**
```tlv
\m5_TLV_version 1d: tl-x.org
\m5
\SV
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   
   $out = $sel[0] ? $a : $sel[1] ? $b : $sel[2] ? $c : $d;
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```
**makerchip link:** [mux4:1](https://www.makerchip.com/sandbox/0W6fjhnMo/0wjhGR8)
**output**
**image**

#### vectors
**code**
```tlv
m5_TLV_version 1d: tl-x.org
\m5
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   $out[4:0] = $in1[3:0] +$in2[3:0];
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```
**makerchip link** [vectors](https://www.makerchip.com/sandbox/0W6fjhnMo/0Wnh5y3)
**output**
**image**

####  pythogoras theorm

**code**
```tlv
\m5_TLV_version 1d: tl-x.org
\m5
\SV
   `include "sqrt32.v"
   m5_makerchip_module   
\TLV  
   $aa_sq[7:0] = $aa ** 2;
   $bb_sq[7:0] = $bb ** 2;
   $cc_sq[8:0] = $aa_sq + $bb_sq;
   $cc[4:0] = sqrt($cc_sq);
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```
**makerchip** [pythogoras therom](https://www.makerchip.com/sandbox/0W6fjhnMo/0Y6hL6x)
**output**
**image**

#### Combinational calaculator
**code**
```tlv
\m5_TLV_version 1d: tl-x.org
\m5
\SV
  
   m5_makerchip_module 
\TLV
   $reset = *reset;
   
   $sel[1:0] = *cyc_cnt[1:0];
   $val1[31:0] = $rand1[3:0];
   $val2[31:0] = $rand2[3:0];
   $sum[31:0] = $val1[31:0] + $val2[31:0];
   $diff[31:0] = $val1[31:0] - $val2[31:0];
   $prod[31:0] = $val1[31:0] * $val2[31:0];
   $quot[31:0] = $val1[31:0] / $val2[31:0];
   $out[31:0] = ($sel == 2'b00) ? $sum :
       ($sel == 2'b01) ? $diff :
       ($sel == 2'b10) ? $prod :
                         $quot; 
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```

**makerchip** [combinational_calc](https://www.makerchip.com/sandbox/0W6fjhnMo/0X6hXMz)
**output**
**image**


  
  

    
