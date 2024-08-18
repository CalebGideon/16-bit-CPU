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

  <p><b>NOTE!</b>Hopefully with time, this README will cover every aspect of this image, as the complexity can seem incredibly daunting, but with adequate knowledge of each component, the process of CPU design is learnable. While this document will not go over what multiplexers are, demultiplexers, tunnels, bus's, sub-circuits and the basics of Logisim, I will try my best to go over the abstractable concepts of what exactly the CPU needs</p>

  <br>
  
  <h4><b>Program Counter (PC)</b></h4>

  <img src="README_IMG's/PC.jpg">

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
