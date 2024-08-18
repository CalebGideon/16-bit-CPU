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
        <li><a href="#download">Download -> Table of Opcodes</a></li>
        <li><a href="#parameters">Example programs</a></li>
        <li><a href="#creating">Custom Assembly Language</a></li>
      </ul>
    </li>
  </ul>
</div>


### Opcodes

| Opcode | Instruction | Description               |
|--------|-------------|---------------------------|
| 0x00   | NOP         | No operation              |
| 0x01   | MOV         | Move data                 |
| 0x02   | ADD         | Add two operands          |
| 0x03   | SUB         | Subtract two operands     |
| 0x04   | MUL         | Multiply two operands     |
| 0x05   | DIV         | Divide two operands       |
| 0x06   | JMP         | Jump to address           |
| 0x07   | JEQ         | Jump if equal             |
| 0x08   | JNE         | Jump if not equal         |
| 0x09   | AND         | Logical AND                |
| 0x0A   | OR          | Logical OR                 |
| 0x0B   | XOR         | Logical XOR                |
| 0x0C   | NOT         | Logical NOT                |
| 0x0D   | CMP         | Compare two operands      |
| 0x0E   | PUSH        | Push value onto stack     |
| 0x0F   | POP         | Pop value from stack      |
| 0x10   | CALL        | Call subroutine           |
| 0x11   | RET         | Return from subroutine    |
| 0x12   | INC         | Increment                  |
| 0x13   | DEC         | Decrement                  |
| 0x14   | SHL         | Shift left                 |
| 0x15   | SHR         | Shift right                |
| 0x16   | MULS        | Multiply with signed      |
| 0x17   | DIVS        | Divide with signed        |
