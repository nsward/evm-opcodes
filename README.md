# EVM Opcodes
An updated version of the EVM reference page at [ethervm.io](https://ethervm.io/). Also drawn from the [Yellow Paper](https://ethereum.github.io/yellowpaper/paper.pdf) and the [Jello Paper](https://jellopaper.org/evm.html).

| Hex | Name        | Gas | Stack In            | Stack Out             | Mem / Storage Out     | Notes |
| :---: | :---      | :---: | :---              | :---                  | :---                  | :--- |
|   |               |   | top, bottom      | top, bottom           ||
00  | STOP          |   |                       |                       || halt execution
01  | ADD           |   | a, b                  | a + b	                || (u)int256 addition modulo 2\*\*256
02  | MUL           |   | a, b                  | a \* b                || (u)int256 multiplication modulo 2\*\*256
03  | SUB           |   | a, b                  | a - b	                || (u)int256 addition modulo 2\*\*256
04  | DIV           |   | a, b                  | a // b                || uint256 division
05  | SDIV          |   | a, b                  | a // b                || int256 division
06  | MOD           |   | a, b                  | a % b                 || uint256 modulus
07  | SMOD          |   | a, b                  | a % b                 || int256 modulus
08  | ADDMOD        |   | a, b, N               | (a + b) % N           || (u)int256 addition modulo N
09  | MULMOD        |   | a, b, N               | (a * b) % N           || (u)int256 multiplication modulo N
0A  | EXP           |   | a, b                  | a \*\* b              || uint256 exponentiation modulo 2\*\*256
0B  | SIGNEXTEND    |   | b, x                  | SIGNEXTEND(x, b)      || sign extend `x` from `(b + 1) * 8` bits to 256 bits.
0C  | *invalid*
0D  | *invalid*
0E  | *invalid*
0F  | *invalid*
10  | LT            |   | a, b                  | a < b                 || uint256 less-than
11  | GT            |   | a, b                  | a > b                 || uint256 greater-than
12  | SLT           |   | a, b                  | a < b                 || int256 less-than
13  | SGT           |   | a, b                  | a > b                 || int256 greater-than
14  | EQ            |   | a, b                  | a == b                || (u)int256 equality
15  | ISZERO        |   | a                     | a == 0                || (u)int256 iszero
16  | AND           |   | a, b                  | a && b                || bitwise AND
17  | OR            |   | a, b                  | a \|\| b              || bitwise OR
18  | XOR           |   | a, b                  | a ^ b                 || bitwise XOR
19  | NOT           |   | a                     | ~a                    || bitwise NOT
1A  | BYTE          |   | i, x                  | (x >> (248 - i * 8)) && 0xFF || `i`th byte of (u)int256 `x`, from the left
1B  | SHL           |   | shift, val            | val << shift          || shift left
1C  | SHR           |   | shift, val            | val >> shift          || logical shift right
1D  | SAR           |   | shift, val            | val >> shift          || arithmetic shift right
1E  | *invalid*
1F  | *invalid*
20  | SHA3          |   | ost, len           | keccak256(mem[ost:ost+len]) || keccak256
21  | *invalid*
22  | *invalid*
23  | *invalid*
24  | *invalid*
25  | *invalid*
26  | *invalid*
27  | *invalid*
28  | *invalid*
29  | *invalid*
2A  | *invalid*
2B  | *invalid*
2C  | *invalid*
2D  | *invalid*
2E  | *invalid*
2F  | *invalid*
30  | ADDRESS       |   |                       | address(this)         || address of executing contract
31  | BALANCE       |   | addr                  | addr.balance          || balance, in wei
32  | ORIGIN        |   |                       | tx.origin             || address that originated the tx
33  | CALLER        |   |                       | msg.sender            || address of msg sender
34  | CALLVALUE     |   |                       | msg.value             || msg value, in wei
35  | CALLDATALOAD  |   | idx                   | msg.data[idx:idx+32]  || read word from msg data at index `idx`
36  | CALLDATASIZE  |   |                       | len(msg.data)         || length of msg data, in bytes
37  | CALLDATACOPY  |   | dstOst, ost, len      |                       | mem[dstOst:dstOst+len= msg.data[ost:ost+len | copy msg data
38  | CODESIZE      |   |                       | len(this.code)        || length of executing contract's code, in bytes
39  | CODECOPY      |   | dstOst, ost, len      |                       | mem[dstOst:dstOst+len] = this.code[ost:ost+len] | copy executing contract's bytecode
3A  | GASPRICE      |   |                       | tx.gasprice           || gas price of tx, in wei per unit gas
3B  | EXTCODESIZE   |   | addr                  | len(addr.code)        || size of code at addr, in bytes
3C  | EXTCODECOPY   |   |addr, dstOst, ost, len |                       | mem[dstOst:dstOst+len] = addr.code[ost:ost+len] | copy code from `addr`
3D  |RETURNDATASIZE |   |                       | size                  || size of returned data from last external call, in bytes
3E  |RETURNDATACOPY |   | dstOst, ost, len      |                       | mem[dstOst:dstOst+len] = returndata[ost:ost+len] | copy returned data from last external call
3F  | EXTCODEHASH   |   | addr                  | hash                  || hash = addr.exists ? keccak256(addr.code) : 0
40  | BLOCKHASH     |   | blockNum              |block.blockHash(blockNum)||
41  | COINBASE      |   |                       | block.coinbase        || address of miner of current block
42  | TIMESTAMP     |   |                       | block.timestamp       || timestamp of current block
43  | NUMBER        |   |                       | block.number          || number of current block
44  | DIFFICULTY    |   |                       | block.difficulty      || difficulty of current block
45  | GASLIMIT      |   |                       | block.gaslimit        || gas limit of current block
46  | CHAINID       |   |                       | chain\_id             || push current [chain id](https://eips.ethereum.org/EIPS/eip-155) onto stack
47  | SELFBALANCE   |   |                       | address(this).balance || balance of executing contract, in wei
48  | *invalid*
49  | *invalid*
4A  | *invalid*
4B  | *invalid*
4C  | *invalid*
4D  | *invalid*
4E  | *invalid*
4F  | *invalid*
50  | POP           |   | \_anon                |                       || remove item from top of stack and discards it
51  | MLOAD         |   | ost                   | mem[ost:ost+32]       || read word from memory at offset `ost`
52  | MSTORE        |   | ost, val              |                       | mem[ost:ost+32] = val | write a word to memory
53  | MSTORE8       |   | ost, val              |                       | mem[ost] = val && 0xFF | write a single byte to memory
54  | SLOAD         |   | key                   | storage[key]          || read word from storage
55  | SSTORE        |   | key, val              |                       | storage[key] = val | write word to storage
56  | JUMP          |   | dst                   |                       || `$pc = dst`
57  | JUMPI         |   | dst, condition        |                       || `$pc = condition ? dst : $pc + 1`
58  | PC            |   |                       | $pc                   || program counter
59  | MSIZE         |   |                       | len[mem]              || size of memory in current execution context, in bytes
5A  | GAS           |   |                       | gasRemaining          ||
5B  | JUMPDEST      |   |                       |                       || mark valid jump destination
5C  | *invalid*
5D  | *invalid*
5E  | *invalid*
5F  | *invalid*
60  | PUSH1         |   |                       | uint8                 || push 1-byte value onto stack
61  | PUSH2         |   |                       | uint16                || push 2-byte value onto stack
62  | PUSH3         |   |                       | uint24                || push 3-byte value onto stack
63  | PUSH4         |   |                       | uint32                || push 4-byte value onto stack
64  | PUSH5         |   |                       | uint40                || push 5-byte value onto stack
65  | PUSH6         |   |                       | uint48                || push 6-byte value onto stack
66  | PUSH7         |   |                       | uint56                || push 7-byte value onto stack
67  | PUSH8         |   |                       | uint64                || push 8-byte value onto stack
68  | PUSH9         |   |                       | uint72                || push 9-byte value onto stack
69  | PUSH10        |   |                       | uint80                || push 10-byte value onto stack
6A  | PUSH11        |   |                       | uint88                || push 11-byte value onto stack
6B  | PUSH12        |   |                       | uint96                || push 12-byte value onto stack
6C  | PUSH13        |   |                       | uint104               || push 13-byte value onto stack
6D  | PUSH14        |   |                       | uint112               || push 14-byte value onto stack
6E  | PUSH15        |   |                       | uint120               || push 15-byte value onto stack
6F  | PUSH16        |   |                       | uint128               || push 16-byte value onto stack
70  | PUSH17        |   |                       | uint136               || push 17-byte value onto stack
71  | PUSH18        |   |                       | uint144               || push 18-byte value onto stack
72  | PUSH19        |   |                       | uint152               || push 19-byte value onto stack
73  | PUSH20        |   |                       | uint160               || push 20-byte value onto stack
74  | PUSH21        |   |                       | uint168               || push 21-byte value onto stack
75  | PUSH22        |   |                       | uint176               || push 22-byte value onto stack
76  | PUSH23        |   |                       | uint184               || push 23-byte value onto stack
77  | PUSH24        |   |                       | uint192               || push 24-byte value onto stack
78  | PUSH25        |   |                       | uint200               || push 25-byte value onto stack
79  | PUSH26        |   |                       | uint208               || push 26-byte value onto stack
7A  | PUSH27        |   |                       | uint216               || push 27-byte value onto stack
7B  | PUSH28        |   |                       | uint224               || push 28-byte value onto stack
7C  | PUSH29        |   |                       | uint232               || push 29-byte value onto stack
7D  | PUSH30        |   |                       | uint240               || push 30-byte value onto stack
7E  | PUSH31        |   |                       | uint248               || push 31-byte value onto stack
7F  | PUSH32        |   |                       | uint256               || push 32-byte value onto stack
80  | DUP1          |   | val                   | val, val              || clone 1st value on stack
81  | DUP2          |   | \_, val               | val, \_, val          || clone 2nd value on stack
82  | DUP3          |   | \_, \_, val           | val, \_, \_, val      || clone 3rd value on stack
83  | DUP4          |   | \_, \_, \_, val       | val, \_, \_, \_, val  || clone 4th value on stack
84  | DUP5          |   | ..., val              | val, ..., val         || clone 5th value on stack
85  | DUP6          |   | ..., val              | val, ..., val         || clone 6th value on stack
86  | DUP7          |   | ..., val              | val, ..., val         || clone 7th value on stack
87  | DUP8          |   | ..., val              | val, ..., val         || clone 8th value on stack
88  | DUP9          |   | ..., val              | val, ..., val         || clone 9th value on stack
89  | DUP10         |   | ..., val              | val, ..., val         || clone 10th value on stack
8A  | DUP11         |   | ..., val              | val, ..., val         || clone 11th value on stack
8B  | DUP12         |   | ..., val              | val, ..., val         || clone 12th value on stack
8C  | DUP13         |   | ..., val              | val, ..., val         || clone 13th value on stack
8D  | DUP14         |   | ..., val              | val, ..., val         || clone 14th value on stack
8E  | DUP15         |   | ..., val              | val, ..., val         || clone 15th value on stack
8F  | DUP16         |   | ..., val              | val, ..., val         || clone 16th value on stack
90  | SWAP1         |   | a, b                  | b, a                  ||
91  | SWAP2         |   | a, \_, b              | b, \_, a              ||
92  | SWAP3         |   | a, \_, \_, b          | b, \_, \_, a          ||
93  | SWAP4         |   | a, \_, \_, \_, b      | b, \_, \_, \_, a      ||
94  | SWAP5         |   | a, ..., b             | b, ..., a             ||
95  | SWAP6         |   | a, ..., b             | b, ..., a             ||
96  | SWAP7         |   | a, ..., b             | b, ..., a             ||
97  | SWAP8         |   | a, ..., b             | b, ..., a             ||
98  | SWAP9         |   | a, ..., b             | b, ..., a             ||
99  | SWAP10        |   | a, ..., b             | b, ..., a             ||
9A  | SWAP11        |   | a, ..., b             | b, ..., a             ||
9B  | SWAP12        |   | a, ..., b             | b, ..., a             ||
9C  | SWAP13        |   | a, ..., b             | b, ..., a             ||
9D  | SWAP14        |   | a, ..., b             | b, ..., a             ||
9E  | SWAP15        |   | a, ..., b             | b, ..., a             ||
9F  | SWAP16        |   | a, ..., b             | b, ..., a             ||
A0  | LOG0          |   | ost, len              |                       || LOG0(memory[ost:ost+len])
A1  | LOG1          |   | ost, len, topic0      |                       || LOG1(memory[ost:ost+len], topic0)
A2  | LOG2          |   | ost, len, topic0, topic1 |                    || LOG1(memory[ost:ost+len], topic0, topic1)
A3  | LOG3          |   | ost, len, topic0, topic1, topic2 |            || LOG1(memory[ost:ost+len], topic0, topic1, topic2)
A4  | LOG4          |   | ost, len, topic0, topic1, topic2, topic3 |    || LOG1(memory[ost:ost+len],&#160;topic0,&#160;topic1,&#160;topic2,&#160;topic3)
A5  | *invalid*
A6  | *invalid*
A7  | *invalid*
A8  | *invalid*
A9  | *invalid*
AA  | *invalid*
AB  | *invalid*
AC  | *invalid*
AD  | *invalid*
AE  | *invalid*
AF  | *invalid*
B0  | *invalid*
B1  | *invalid*
B2  | *invalid*
B3  | *invalid*
B4  | *invalid*
B5  | *invalid*
B6  | *invalid*
B7  | *invalid*
B8  | *invalid*
B9  | *invalid*
BA  | *invalid*
BB  | *invalid*
BC  | *invalid*
BD  | *invalid*
BE  | *invalid*
BF  | *invalid*
C0  | *invalid*
C1  | *invalid*
C2  | *invalid*
C3  | *invalid*
C4  | *invalid*
C5  | *invalid*
C6  | *invalid*
C7  | *invalid*
C8  | *invalid*
C9  | *invalid*
CA  | *invalid*
CB  | *invalid*
CC  | *invalid*
CD  | *invalid*
CE  | *invalid*
CF  | *invalid*
D0  | *invalid*
D1  | *invalid*
D2  | *invalid*
D3  | *invalid*
D4  | *invalid*
D5  | *invalid*
D6  | *invalid*
D7  | *invalid*
D8  | *invalid*
D9  | *invalid*
DA  | *invalid*
DB  | *invalid*
DC  | *invalid*
DD  | *invalid*
DE  | *invalid*
DF  | *invalid*
E0  | *invalid*
E1  | *invalid*
E2  | *invalid*
E3  | *invalid*
E4  | *invalid*
E5  | *invalid*
E6  | *invalid*
E7  | *invalid*
E8  | *invalid*
E9  | *invalid*
EA  | *invalid*
EB  | *invalid*
EC  | *invalid*
ED  | *invalid*
EE  | *invalid*
EF  | *invalid*
F0  | CREATE        |   | val, ost, len                                     | addr          || addr = keccak256(rlp([address(this), this.nonce]))
F1  | CALL          |   | gas,&#160;addr,&#160;val,&#160;argOst,&#160;argLen,&#160;retOst,&#160;retLen | success        | mem[retOst:retOst+retLen] = returndata |
F2  | CALLCODE      |   | gas, addr, val, argOst, argLen, retOst, retLen    | success       | mem[retOst:retOst+retLen]&#160;=&#160;returndata | same&#160;as&#160;DELEGATECALL,&#160;but&#160;does&#160;not&#160;propogate&#160;original&#160;msg.sender&#160;and&#160;msg.value
F3  | RETURN        |   | ost, len                                          |               || return mem[ost:ost+len]
F4  | DELEGATECALL  |   | gas, addr, argOst, argLen, retOst, retLen         | success       | mem[retOst:retOst+retLen] = returndata |
F5  | CREATE2       |   | val, ost, len, salt                               | addr          || addr = keccak256(0xff ++ address(this) ++ salt ++ keccak256(mem[ost:ost+len]))[12:]
F6  | *invalid*
F7  | *invalid*
F8  | *invalid*
F9  | *invalid*
FA  | STATICCALL    |   | gas, addr, argOst, argLen, retOst, retLen         | success       | mem[retOst:retOst+retLen] = returndata |
FB  | *invalid*
FC  | *invalid*
FD  | REVERT        |   | ost, len                                          |               || revert(mem[ost:ost+len])
FE  | INVALID       |   |                                                   |               || designated invalid opcode - [EIP-141](https://eips.ethereum.org/EIPS/eip-141)
FF  | SELFDESTRUCT  |   | addr                                              |               || destroy contract and sends all funds to `addr`
