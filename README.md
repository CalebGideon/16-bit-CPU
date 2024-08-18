# 16-bit-CPU with Custom Assembly Language

A functioning 16-BIT unisigned CPU made in Logisim with visual display for output of numerical calculations. Supports complex jumping, bitwise operations with custom assembly language writing

<div>
  <h2>Table of Contents</h2>
  <ul>
    <li><a href="#section1">Breakdown</a>
      <ul>
        <li><a href="#purpose">Purpose</a></li>
        <li><a href="#pipeline">Pipeline</a></li>
        <li><a href="#limitations">Limitations</a></li>
      </ul>
    </li>
    <li><a href="#section2">Instruction Set</a>
      <ul>
        <li><a href="#opcodes">Table of Opcodes</a></li>
        <li><a href="#parameters">Compound Opcode Complexity</a></li>
        <li><a href="#parameters">Example programs</a></li>
        <li><a href="#creating">Custom Assembly Language</a></li>
      </ul>
    </li>
  </ul>
</div>

<div>
  <h3 id="purpose">Purpose</h3>
  <p>The CPU design is developed entirely in Logisim: <a = "https://sourceforge.net/projects/circuit/"><b>Click here to download the latest version</b></a></p>
  <br>
  <p>This repository provides a detailed look into the development for a 16-bit unsigned CPU. The idea is to teach people about the fundamentals of hardware development, in addition to showcasing assembly to machine code conversion, which tends to be overlooked by most CS graduates. The repository will take a look at:</p>
  <ul>
    <li>The different opcodes a CPU might use</li>
    <li>The pipeline of a CPU including: </li>
    <ul>
      <li>ROM to RAM parallel storage similar to the Harvards System</li>
      <li>Double Dabble algorithm to convert Binary to Binary Coded Decimal <b>BCD</b></li>
      <li>How jumping works within CPU architecture, and more importantly, how it works with limited opcode space</li>
      <li>How to generate immediate value storage</li>
      <li>A look into ALU, General Register and Flag Register design</li>
      <li>How to develop a control unit</li>
    </ul>
    <li>How to create an assembly language to write programs in human readable and not machine code (screw that!)</li>
    <li>How to display data, and different clock speeds to manage complex algorithms such as Double Dabble</li>
  </ul>

  <br>

  <p><b>Hopefully you learn something, and feel free to download the CPU in full. If you're uploading it to people, please provide me credit, but otherwise, rip it to shreds and learn as much as you can!</b></p>
  
</div>

<div>
  <h3 id="pipeline">Pipeline</h3>

  <img src="Overview_CPU.jpg">

  <br>

  <p><b>NOTE!</b>Hopefully with time, this README will cover every aspect of this image, as the complexity can seem incredibly daunting, but with adequate knowledge of each component, the process of CPU design is learnable. While this document will not go over what multiplexers are, demultiplexers, tunnels, bus's, sub-circuits, spillters, and the basics of Logisim, I will try my best to go over the abstractable concepts of what exactly the CPU needs</p>

  <br>
  
  <h4><b>Program Counter (PC)</b></h4>

  <img src="README_IMG's/PC.jpg">

  <p><b>It all begins with a clock. MASTER_CLOCK ticks, incrementing the entire CPU's pipeline by one iteration based on a High/Low frequency shift. On the positive tick, the following occurs:</b></p>

  <ol>
    <li>A signal is sent to the general register to activate its ability to have a value written to it (the box with 000 to the right of MUX)</li>
    <li>The MUX -> multiplexer to its left, takes in four values, with the choice of 4 values decided by a selector -> The JUMP/BOUNCE/JUMP_NZERO opcodes./b>:</li>
    <ul>
      <li>When JUMP/BOUNCE/JUMP_NZERO are all 0, the selector value is -> 00. Thus, the program counter sends a value to the incrementer (box with cin/cout), and increments the PC's current value (lets say 12), by 1 -> (how by one? The constant 0001 is sent through) This gets fed back into the general register, and increments the ROM for later </li>
      <li>When JUMP is true, the selector value is -> 01. Thus, the program counter will simply send through the 16-bit jump address that shifts the RAM memory to a different location. (RAM at memory location 12? jump address is 1? Program Counter becomes 0001!)</li>
      <li>When Bouncer is true, the selector value is -> 10. Thus, the program counter will check whether a previous Comparison yielded true or false (Think if/while loop conditions). If true, it jumps the program counter to a memory location, else (if/while loop ends), it switch's back to the default 00's single increment logic</li>
      <li>When JUMP_NZERO is true, the selector value is -> 11. (Note: This can be seen by the two or gates to the right of JUMP/BOUNCER/JUMP_NZERO, setting both results to true in this case). Here, the program will check if a zero flag is set to true. If so, then a for loop has just ended (think for i less than size, where i is now 10 and size is 10), else it defaults to single 00 increment</li>
    </ul>
  </ol>

  <br>

  <h4><b>Read Only Memory (ROM)</b></h4>

  <img src="README_IMG's/ROM.jpg">

  <br>
  
  <h4><b>Random Access Memory (RAM)</b></h4>

   <img src="README_IMG's/RAM.jpg">

  <br>
  
  <h4><b>RAM Check</b></h4>

   <img src="README_IMG's/RAMON.jpg">

   <br>

  <h4><b>COPY</b></h4>

   <img src="README_IMG's/COPY.jpg">

   <br>

  <h4><b>Control Unit (CU)</b></h4>

   <img src="README_IMG's/Control_Unit.jpg">

   <br>

  <h4><b>Flag Register (FR)</b></h4>

   <img src="README_IMG's/Flag_Register.jpg">

   <br>

  <h4><b>ROM Immediate</b></h4>

   <img src="README_IMG's/ROM_IM.jpg">

   <br>

  <h4><b>RAM Immediate</b></h4>

   <img src="README_IMG's/RAM_IM.jpg">

   <br>

  <h4><b>General Register (GR)</b></h4>

   <img src="README_IMG's/General_Register.jpg">

   <br>

  <h4><b>Arithmetic Logic Unit (ALU)</b></h4>

   <img src="README_IMG's/ALU.jpg">

   <br>

  <h4><b>Double Dabble Pipeline (DDP)</b></h4>

   <img src="README_IMG's/View_Pipe.jpg">

   <br>

  <h4><b>Visual Display</b></h4>
  
   <img src="README_IMG's/Visual_Dis.jpg">

   <br>
  
</div>

<div>

<h3 id="opcodes">Table of Opcodes</h3>
<p>Due to the CPU instruction register memory address being split into 4 bits for its opcode, the CPU only possesses 16. Additional functionalities such as swapping registers can be achieved via compound opcode complexity (COC -> discussed later. E.G. for now, two or commands and an additional register simulating SWAP)</p>

<p><b>Below is a table consisting of the different opcodes, their hex equivalent, and the description of what each achieves</b></p>
</div>

### Opcodes

| Opcode | Instruction | Description               |
|--------|-------------|---------------------------|
| 0x00   | NOP         | No operation              |
| 0x01   | AND         | Logical AND               |
| 0x02   | OR          | Logical OR                |
| 0x03   | XOR         | Logical XOR               |
| 0x04   | XNOR        | Logical XNOR              |
| 0x05   | ADD         | Adds two numbers          |
| 0x06   | SUB         | Subtracts two numbers     |
| 0x07   | MUL         | Multiplies two numbers    |
| 0x08   | DIV         | Divides two numbers       |
| 0x09   | COMP        | Compares two numbers      |
| 0x0A   | LOAD        | Loads data from register to RAM |
| 0x0B   | JUMP_NZERO  | Jumps if not zero         |
| 0x0C   | WRITE       | Writes data from ROM/RAM to register |
| 0x0D   | BOUNCER     | Jumps based on last condition |
| 0x0E   | JUMP        | Unconditional jump        |
| 0x0F   | COPY        | Copies data from ROM to RAM |
