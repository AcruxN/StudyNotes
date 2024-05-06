# CSLLT NOTE

## Table of Contents

- [Lecture 1](#lecture-1)
  - [Register](#register)
  - [GPR (General purpose register) [User visible register]](#gpr-general-purpose-register-user-visible-register)
  - [SPR (Special purpose register) [User invisible register]](#spr-special-purpose-register-user-invisible-register)
  - [Steps for ASM programming](#steps-for-asm-programming)
- [Lecture 2](#lecture-2)
  - [Services](#services)
  - [In a CPU](#in-a-cpu)
  - [Segments Register](#segments-register)
  - [Assembly coding, DOS APIs](#assembly-coding-dos-apis)
  - [Pseudo-Ops](#pseudo-ops)
  - [Assembly Example](#assembly-example)
  - [Addressing Modes in 8086](#addressing-modes-in-8086)
- [Lecture 3](#lecture-3)
  - [Little Man Computer (LMC)](#little-man-computer-lmc)
  - [Translator (System translator)](#translator-system-translator)
  - [von Neumann Architecture Guidelines](#von-neumann-architecture-guidelines)
  - [LMC Instruction Set](#lmc-instruction-set)


## Lecture 1

### Register

- **Memory slot in the CPU**
- **Slot is permanent, data is temporary**
- **To hold and store values**

---

### GPR (General purpose register) [User visible register]

- **Accumulator register (AX = AL + AH)**
  - To perform arithmetic addition and subtraction
  - To hold intermediate value
  - Also known as arithmetic register
  - Size of AL & AH are 1 bit

- **Base register (BX = BL + BH)**
  - To hold or store base address
  - To hold or store base value

- **Counter register (CX)**
  - To hold count values
  - To count repeated data/values
    - Example: cache memory, loop values

- **Data register (DX)**
  - To handle data
  - To hold/store data
  - To perform multiplication and division

- **Source index register (SI)**
  - To handle source index address (Example: array index)

- **Destination index register (DI)**
  - To handle destination index address

- **Base pointer register (BP)**
  - To handle base pointer values (address)

- **Stack pointer register (SP)**
  - To handle stack address

---

### SPR (Special purpose register) [User invisible register]

- **Instruction register (IR)**
  - To point to the current instruction
  - Also known as high-speed register

- **Program counter register (PCR/IPR)**
  - To point to the address of the next instruction
  - Also known as instruction pointer register

- **Memory address register (MAR)**
  - To hold all memory addresses

- **Memory data register (MDR)**
  - To hold all memory data
  - Also known as memory buffer register (MBR)

- **Status register (SR)**
  - To indicate the status of CPU
  - To indicate either internal or external error
  - Also known as control register (CR) / flag register (FR) / program status word (PSW)
    - Control register [status of external system]
    - Flag register [Zero flag | parity flag | overflow flag | carry flag | half-carry flag | sign flag]

---

### Steps for ASM programming

1. Create ASM file, save.
2. Compile with TASM, get OBJ file.
3. Link with TLINK, get EXE.
4. Run the EXE.

---

- `.model` small / medium / compact / large / huge
  - If not specified, 1KB will be allocated.
- Assembly is non-case sensitive.

---

## Lecture 2

### Services

- **Services** are called as predefined functions, which are created by computer manufacturers (Intel, AMD).
- It facilitates communication between layers:
  - Hardware layer
  - Software layer
  - Operating system layer
  - BIOS layer
- **Registers** are mainly used to facilitate services.

### In a CPU

- **CU (Control Unit)** - Control unit controls the activity of the CPU, makes synchronization available for other components.
- **ALU (Arithmetic/Logical Unit)** - Perform arithmetic (+-) and logic (<>==).

### Segments Register

- **B4 segment**
  - CS - Code Segments
  - SS - Stack Segment
  - DS - Data Segment
  - ES - Extra Segment
- **Additional Segments**
  - FS - Extra Segment
  - GS - Microsoft's Extra Segment

### Assembly coding, DOS APIs

```assembly
mov ah,02 ; Display character
mov ah,09 ; Display string
mov ah,01 ; Character input
mov ah,0ah ; String input
```

### Pseudo-Ops

- EQU - Enables us to create constant
- DB - Allows us to create a variable which contains a byte of data (8 bits)
- DW - Allows us to create a variable which contains a word data (16 bits)
- DD - Allows us to create a variable which contains two words (32 bits)
- **Note**
- int takes 2 byte
- char takes 1 byte
- float takes 4 byte

### Assembly Example

```assembly
.model small
.stack 100h
.DATA
msg db "CSLLT" ; Every character is stored in 1 byte [DB]
cr EQU 0Dh ; Carriage return | cr = 13
lf EQU 0Ah ; Line feed | lf = 10
oldage EQU 80 ;
...
```

### Addressing Modes in 8086

The way of specifying data/operand to be operated by an instruction is known as addressing modes. This specifies that the given data is an immediate data or an address.

#### 11 Addressing Modes

##### Register Mode

- Source and destination operand must be register
  - Example: `mov ax, bx`, `xor ax,dx`, `add al, bl`

##### Immediate Mode

- The source operand can be 8 bit or 16 bit data, destination operand can never be immediate data
  - Example: `mov ax,2000`, `mov cl,0A`, `mov al,45`, `AND ax,000`

##### Direct Mode or Displacement Mode

##### Register Indirect Mode

##### Based Indexed Mode

##### Indexed Mode

##### Based Mode

##### Based Indexed Displacement Mode

##### String Mode

##### Input / Output Mode

##### Relative Mode

##### example

```
_________________________________
mov    ah,   02
 |         \             \
operation  register     value
_________________________________
```

## Lecture 3

### Little Man Computer (LMC)

- Known as computer simulator & computer emulator (toy computer)
- Depicts & resembles operation of real CPU
- CPU simlator that models a simple computer using the von Neumann architecture and memory use

### Translator (System translator)

A set of programs that translate user instructions into machine understandable instructions:
Translator must know the language of the program (programming language) and the language of the cpu (instruction set)

1. Compiler
   - Translates high-level instructions into intermediate object code
   - Translates all instructions at once
   - Examples: JavaC, TurboC, MicrosoftC

2. Interpreter
   - Translates high-level instructions into machine understandable code
   - Translates line by line instructions
   - Example: Java, Python

3. Assembler
   - Translates low-level instructions into machine understandable code
   - Translates all instructions at once
   - Example: TASM, MASM, SASM, NASM

4. Linker
   - Sub translator that translates intermediate object code (symbolic code) into machine understandable code (executable code)
   - Translates intermediate object code all at once
   - Example: tlink, mlink, slink

### von Neumann Architecture Guidelines

- Store program concepts
  - Allows computer to store data and instruction in its memory
- Linear memory address
  - Sequential memory address
  - Continuous memory allocation
  - 100 memory spaces in LMC (00 - 99) to hold or store data
- Sequential processing of instructions
  - All instructions will be executed one by one (sequentially)
- Independence of data & address
  - Both data and address are located separately
- Functional computer organization
  - CU (Control Unit) + ALU (Arithmetical Logical Unit) + MU (Memory Unit)

### LMC Instruction Set

- Follows 3 decimal values
  - 1st decimal is Opcode (operation code)
  - 2nd decimal is operand (memory data / address)
  - 3rd decimal is operand (memory data / address)

- OPCODE 1: Addition
- OPCODE 2: Subtraction
- OPCODE 3: Store operation
- OPCODE 4: Noting
- OPCODE 5: Load
- OPCODE 6: BRU (Branch Unconditionally)
- OPCODE 7: BRZ (Branch on Zero)
- OPCODE 8: BRP (Branch on Positive)
- OPCODE 901: Input | 902: Output
- OPCODE 00: Stop / Halt

#### Sample Addition

```LMC
NO OPCODE NOTES
00 901  1st Input
01 350  Store it in 50th
02 901  2nd Input
03 150  ADD
04 902  Display
05 000  Stop
```

#### Sample Subtraction

```LMC
NO OPCODE NOTES
00 901  1st Input
01 350  Store it in 50th
02 901  2nd Input
03 250  Substraction
04 902  Display
05 000  Stop
```

- **(2nd input - 1st input)**

#### Sample If Statement

```LMC
NO OPCODE NOTES
00 901  1st Input
01 350  Store it in 50th
02 901  2nd Input
03 380  Store it in 80th
04 250  Substraction (b-a)=+-ve
05 809   Go to line 09
06 550  Load the 50th 
07 
08
09 902  Display
010 000  Stop
```

- **(2nd input - 1st input)**
