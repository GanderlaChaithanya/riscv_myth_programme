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

### 1. Implemenation of 2:1 mux:
 
**Code**
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
**Markchip ide link:** [mux2:1]( https://www.makerchip.com/sandbox/0W6fjhnMo/0Nxh0Mm)

**output**

| ![mux2:1](././images/multiplexer.png) |
| :--------------------------------------------------: |
|         multiplexer    |



<br>

### 2. Multiplexer with vectors

**Code**
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
**Makerchip ide link:** [mux_with_vectors](https://www.makerchip.com/sandbox/0W6fjhnMo/0r0h8DL)

**output**

| ![mux_with_vectors](././images/mux_with_vectors.png) |
| :--------------------------------------------------: |
|         mux_with_vectors   |



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
**Makerchip ide link:** [mux4:1](https://www.makerchip.com/sandbox/0W6fjhnMo/0wjhGR8)

**output**

| ![mux4](././images/mux4.png) |
| :--------------------------------------------------: |
|         MUX 4:1  |



<br>

### Vectors
**Code**
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
**Makerchip  IDE link:** [vectors](https://www.makerchip.com/sandbox/0W6fjhnMo/0Wnh5y3)

**output**

| ![Vectors](././images/vectors_lab.png) |
| :--------------------------------------------------: |
|         Vectors  |



<br>
### Pythogoras theorm

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
**Makerchip IDE Link** [pythogoras therom](https://www.makerchip.com/sandbox/0W6fjhnMo/0Y6hL6x)

**Output**


| ![pythogoras](././images/pythogoras_theorm.png) |
| :--------------------------------------------------: |
|  pythogoras_theorm      |


<br>

### Combinational calaculator

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

**Makerchip IDE link :** [combinational_calc](https://www.makerchip.com/sandbox/0W6fjhnMo/0X6hXMz)

**output**

| ![combinational_calc](././images/combinational_calc.png) |
| :--------------------------------------------------: |
|  combinational_calc |


<br>

### Sequential circuits implementation

#### Counter 
**code**
```tlv
m5_TLV_version 1d: tl-x.org
\m5

   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   $reset = *reset;
   
   $num[31:0] = $reset ? 1: (>>1$num+1);
   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```
**Makerchip IDE link:** :[counter](https://www.makerchip.com/sandbox/0W6fjhnMo/0Q1hkNK)

**output**

| ![counter](././images/counter.png) |
| :--------------------------------------------------: |
|  counter |


<br>

### Fibonacci_series
**code**
```tlv
\m5_TLV_version 1d: tl-x.org
\m5
\SV
   m5_makerchip_module  
\TLV
   $reset = *reset; 
   $num [31:0] = $reset ? 1:(>>1$num + >>2$num);
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```
**Makerchip IDE link** :[fibonacci_series](https://www.makerchip.com/sandbox/0W6fjhnMo/0P1hK5m)

**output**

| ![fibonacci_series](././images/fibonacci_series.png) |
| :--------------------------------------------------: |
| fibonacci_series  |


<br>

### Sequential calaculator
**code**
```tlv
\m5_TLV_version 1d: tl-x.org
\m5
\SV
   
   m5_makerchip_module  
\TLV
   $mul[3:0] = $val1[1:0] * $val2[1:0];
   $div[3:0] = $val1[1:0] / $val2[1:0];
   $sub[3:0] = $val1[1:0] - $val2[1:0];
   $add[3:0] = $val1[1:0] + $val2[1:0];
   $result[3:0] = $sel[0] ? $add : $sel[1] ? $sub : $sel[2] ? $mul : $div;
   
   $val2[1:0] = *reset ? 0 : >>1$result;
   *passed = cyc_cnt > 30;
   *failed = 1'b0;
\SV
   endmodule
```
**Makerchip IDE link:** [sequntial_calc](https://www.makerchip.com/sandbox/0W6fjhnMo/0Rghvg1)

**output**

| ![seq](././images/seq.png) |
| :--------------------------------------------------: |
| sequential calaculator  |


<br>

### Pipelining:

Pipelining in Makerchip IDE using TL-Verilog allows efficient execution of multiple instructions simultaneously by dividing operations into stages. It uses the |> operator to define pipeline stages, ensuring automatic data flow between them. TL-Verilog simplifies register management, as pipeline registers are inferred automatically. Each stage processes part of the computation, with data moving forward in every clock cycle. This improves performance, reduces complexity, and enhances scalability. Additionally, TL-Verilog efficiently handles forwarding and pipeline hazards. Makerchip IDE provides a simulation and visualization environment, making debugging and optimization easier.


### Pythogaros therom pipeline
**code**
```tlv
\m4_TLV_version 1d: tl-x.org
\SV
      `include "sqrt32.v";
     m4_makerchip_module   
\TLV
   |calc
      @1
         $aa_sq[31:0] = $aa[3:0] * $aa;
         $bb_sq[31:0] = $bb[3:0] * $bb;
      @2
         $cc_sq[31:0] = $aa_sq + $bb_sq;
         
      @3
         $cc[31:0] = sqrt($cc_sq);   
!  *passed = *cyc_cnt > 16'd30;
\SV
   endmodule
```
**Makerchip IDE link:** [pythogoraus_THOERM](https://www.makerchip.com/sandbox/0W6fjhnMo/0JZhqQk)

**output**

| ![pipelining](././images/pipelining.png) |
| :--------------------------------------------------: |
| pipelining  |


<br>

#### Error pipelining
**code**
```tlv
\m5_TLV_version 1d: tl-x.org
\m5
\SV
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   
   |comp
      @1
         $err1 = $bad_input | $illegal_op;
      @2 
         $err1
      @3
         $err2 =$overflow | $err1;
      @4 
         $err2
      @5
         $err2
      @6
         $err3 = $err2 | $div_by_zero;.
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```
**Makerchip IDE link:** [error_pipelining](https://www.makerchip.com/sandbox/0XDfnhkY4/0pghnAg)

**output**

| ![pipelining_lab](././images/pipelinig_lab.png) |
| :--------------------------------------------------: |
|  error pipelining  |


<br>

### Calaculator_counter_Pipeline
**code**
```tlv
\m5_TLV_version 1d: tl-x.org
\m5
\SV
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV 
   |calc
      @0
         
         $N = 32'b0;
         $sum[31:0] = $val1[31:0] + $val2[31:0];
         $diff[31:0] = $val1[31:0] - $val2[31:0];
         $prod[31:0] = $val1[31:0] * $val2[31:0];
         $quot [31:0] = $val1[31:0] / $val2[31:0];
          
         $out[31:0] = $reset ? 0  :  // Reset overrides everything
                      $op[0] ? $sum :
                      $op[1] ? $diff :
                      $op[2] ? $prod :
                      $op[3] ? $quot : $N;
         $cnt = ($reset) ? 0 : (>>1$cnt+1);
         $val1[31:0] = >>1$out;
   *passed = *cyc_cnt > 40;
   
\SV
   endmodule

```
**Makerchip IDE link:** [combinational_calc_pipeline](https://www.makerchip.com/sandbox/0W6fjhnMo/0Z4h5oZ)

**output**

| ![calc_counter](././images/calc_counter.png) |
| :--------------------------------------------------: |
|  Calaculator_counter_Pipeline  |


<br>

### 2-cycle calaculator 
**code**
```tlv
m5_TLV_version 1d: tl-x.org
\m5
\SV
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   |calc
      @1
         $reset = *reset;
         $val1[31:0] = >>2$out[3:0];
         $val2[31:0] = $rand2[3:0];
         $op[1:0] = $rand3[1:0];
         $sum[31:0] = $val1[31:0] + $val2[31:0];
         $diff[31:0] = $val1[31:0] - $val2[31:0];
         $prod[31:0] = $val1[31:0] * $val2[31:0];
         $quot[31:0] = $val1[31:0] / $val2[31:0];        
         $cnt = $reset == 1 ? 1'h0 : >>1$cnt +1;
      @2
         $valid = ($reset| !$cnt);
         $out[31:0] = $valid ==1 ? 32'h0 :
                                        $op[1:0] == 0 ? $sum:
                                        $op[1:0] == 1 ? $diff:
                                        $op[1:0] == 2? $prod :
                                        $quot;
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```
**Makerchip IDE link:** [2-cycle_calaculator](https://www.makerchip.com/sandbox/0W6fjhnMo/0Bgh7ln)

**output**

| ![cycle_calculator](././images/cycle_calculator.png) |
| :--------------------------------------------------: |
|  cycle_calculator |


<br>
### Validity:
In Makerchip IDE, validity in TL-Verilog plays a crucial role in managing transactions within pipeline stages efficiently. Instead of using explicit enable signals, TL-Verilog introduces the %valid signal to determine whether data in a pipeline stage is meaningful and should be processed. This approach automatically controls when operations occur, preventing unnecessary computations on invalid data. In Makerchip, when designing digital circuits, validity ensures that only active transactions propagate through the pipeline, simplifying control logic and eliminating manual enable signal management. As a result, designers can focus on functionality rather than low-level signal handling. By leveraging validity, Makerchip IDE allows for cleaner, optimized, and modular hardware designs, making pipeline implementation more intuitive and error-free. 



### Clock gating:
In TL-Verilog, clock gating is an implicit mechanism that optimizes power consumption by disabling the clock for pipeline stages when they do not contain valid data. Unlike traditional Verilog, where designers manually implement clock enable signals and gating logic, TL-Verilog automates this process using validity signals (%valid). In Makerchip IDE, when %valid is low, the corresponding pipeline stage remains idle, effectively preventing unnecessary toggling of registers and reducing dynamic power consumption. This automatic clock gating mechanism simplifies hardware design, making it more efficient for low-power applications. By eliminating the need for explicit clock control, TL-Verilog allows designers to focus on functionality while ensuring power-efficient execution, making it an ideal choice for modern digital circuit design.


### Calaculating total distance with validity:

**code**
```tlv
\m4_TLV_version 1d: tl-x.org
\SV
    `include "sqrt32.v";
     m4_makerchip_module
\TLV
   |calc
      @1
         $reset = *reset;
      ?$valid
         @1
            $aa_sq[31:0] = $aa[3:0] * $aa;
            $bb_sq[31:0] = $bb[3:0] * $bb;
         @2
            $cc_sq[31:0] = $aa_sq + $bb_sq;
         @3
            $cc[31:0] = sqrt($cc_sq);
      @4
         $tot_dist[63:0] =
              $reset ? '0 :
              $valid ? >>1$tot_dist + $cc :
                        >>1$tot_dist;
         
!  *passed = *cyc_cnt > 16'd30;
   
\SV
endmodule
```
**Makerchip IDE link:**  [distance_calaculator](https://www.makerchip.com/sandbox/0W6fjhnMo/0zmhMm0)

**output**

| ![distance_validity](././images/distance_validty.png) |
| :--------------------------------------------------: |
|  distance_validity |


<br>

### 2- Cycle_calaculator _validity
**code**
```tlv
\m5_TLV_version 1d: tl-x.org
\m5
\SV
  m5_makerchip_module   
\TLV
   |calc
      @1
         $valid = $reset ? '0 : >>1$valid + 1;
         $valid_reset = $valid || $reset; 
         ?$valid
            $val1[31:0] = >>2$out[3:0];
            $val2[31:0] = $rand2[3:0];
            $op[1:0] = $rand3[1:0];
            $sum[31:0] = $val1 + $val2;
            $diff[31:0] = $val1 - $val2;
            $prod[31:0] = $val1 * $val2;
            $quot[31:0] = $val1 / $val2;

      @2
         $out[31:0] = $valid_reset == 1 ? 
                                        $op[1:0] == 0 ? $sum:
                                        $op[1:0] == 1 ? $diff:
                                        $op[1:0] == 2? $prod :
                                        $quot : >>1$out;
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```
**Makerchip IDE link:** [cycle_calaculator](https://www.makerchip.com/sandbox/0W6fjhnMo/0y8hryg)

**output**

| ![2- Cycle_calaculator _validity](././images/cycle_calc_validity.png) |
| :--------------------------------------------------: |
|  2- Cycle_calaculator _validity |









  
  

    
