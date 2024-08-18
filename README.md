

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
