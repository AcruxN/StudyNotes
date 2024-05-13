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
- [Lecture 4](#lecture-4)

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

##### 1. Register Mode

- Source and destination operand must be register
  - Example: `mov ax, bx`, `xor ax, dx`, `add al, bl`

##### 2. Immediate Mode

- The source operand can be 8 bit or 16 bit data, destination operand can never be immediate data (Right operand = source operand)
  - Example: `mov ax, 2000`, `mov cl, 0A`, `mov al, 45`, `AND ax, 000`

##### 3. Direct Mode or Displacement Mode

- Effective address is directly given in the instruction as displacement (Source operand is address)
  - Example: `mov ax, [disp]`, `mov ax, [0500]`

##### 4. Register Indirect Mode

- Effective address is in SI, DI, or BX (Source operand is register that holds address)
  - Example: `mov ax, [DI]`, `mov al, [BX]`, `mov ax, [SI]`

##### 5. Based Indexed Mode

- Effective address is sum of base register and index register
  - Base register: BX, BP
  - Index register: SI, DI
  - Physical memory address is calculated according to the base register
    - Example: `mov al, [BP + SI]`, `mov ax, [BX + DI]`

##### 6. Indexed Mode

- Effective address is sum of index reister and displacement
  - Example: `mov ax, [SI + 2000]`, `mov al, [DI + 3000]`

##### 7. Based Mode

- Effective address is sum of base register and displacement
  - Example: `mov al, [BP + 0100]`

##### 8. Based Indexed Displacement Mode

- Effective address is sum of index register, base registern and displacement
  - Example: `mov al, [SI + BP + 2000]`

##### 9. String Mode

- This addressing mode is related to string instruction.
  In this the value of SI and DI are auto incremented and decremented depending upon the value of directional flag
  - Example: `movs B` (byte moving 8 bits), `movs W` (word moving 16 bits)

##### 10. Input / Output Mode

- This addressing mode is related with input and output operations.
  - Example: `IN A, 45`, `OUT A, 50`

##### 11. Relative Mode

- Effective address is calculated with reference to instruction pointer.
  - Example: `JNZ 8 bit address` (JUMP IF NOT ZERO), `IP = IP + 8 bit address`

##### example

```assembly
_________________________________
mov    ah,             02
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

## Lecture 4

- *Adressing Modes will be in final exam*

### Flow Control

  1. **CMP** - Compare
  2. **JE** - Jump if equal to
  3. **JNE** - Jump if not equal to
  4. **JA** - Jump if above
  5. **JB** - Jump if below

#### Loops

```assembly
.model small
.stack 100h
.code
MAIN PROC
  mov cx, 80   ; set counter to 80
  mov ah,2     ; DOS function to display
  mov dl,'*'   ; character to display

top: int 21h  ; call dos interrupt
  loop top ; repeat

  mov ah, 4Ch  ; DOS terminate
  int 21h      ; return to DOS
MAIN ENDP
end MAIN
```

#### Jumps

- Conditional Jumps
  - Jump statement which moves control to another part of the program depending on the **FLAG** value

```assembly
.model small
.stack. 100h
.code
MAIN PROC
  mov bl, 80   ;
  mov ah,2     ;
  mov dl,'*'   ;

top: int 21h   ; DOS interrupt
  dec bl       ; decrease BL by one
  cmp bl, 0    ; check if BL is zero
  jne top      ; repeat if not equal to zero

  mov ah, 4Ch  ;
  int 21h      ;
MAIN ENDP
end MAIN
```

- Unconditional Jumps
  - Jump statement that moves control to another part of the program even **without FLAG** value
