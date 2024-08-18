# 16-bit-CPU

A functioning 16-BIT unisigned CPU made in Logisim with visual display for output of numerical calculations. Supports complex jumping, bitwise operations with custom assembly language writing

<div>
  <h2>Table of Contents</h2>
  <ul>
    <li><a href="#section1">Breakdown</a>
      <ul>
        <li><a href="#purpose">Purpose</a></li>
        <li><a href="#capabilities">Capabilities</a></li>
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
