# 🧠 Data Types in x86 Assembly (with Clear Little Endian Explanation)

## Introduction

x86 Assembly is one of the lowest-level programming languages still widely used today. It provides direct access to memory and CPU registers, making it ideal for performance-critical applications, embedded systems, and reverse engineering.  
Understanding the core data types and how they are represented in memory is crucial for writing efficient, bug-free assembly code.

In this article, we’ll explore the main data types used in x86 Assembly, including signed vs unsigned values, alignment, and the often misunderstood concept of Little Endian memory layout.

## 📏 Common Data Types in x86 Assembly

- **BYTE (8 bits)**: 0–255 (unsigned) or -128 to 127 (signed)  
- **WORD (16 bits)**: 0–65,535 (unsigned) or -32,768 to 32,767 (signed)  
- **DWORD (32 bits)**: Up to 4,294,967,295 unsigned or -2,147,483,648 to 2,147,483,647 signed  
- **QWORD (64 bits)**: Used in x86-64 for large integers or pointers  
- **FLOAT / DOUBLE**: 32-bit and 64-bit floating-point numbers (IEEE 754 format)

## ➕ Signed vs Unsigned

Signed types use the most significant bit (MSB) to indicate whether the value is positive or negative.

Example:

```
0xFF = 255 (unsigned)
0xFF = -1 (signed)
```

Knowing which version you are using is essential to avoid logic bugs.

## 📐 Data Alignment

Data alignment refers to placing data in memory at addresses that match their size. A 4-byte DWORD should ideally be stored at an address divisible by 4.

### Why is alignment important?

- **Performance**: Aligned access is faster since it matches CPU bus boundaries.
- **Hardware Requirements**: Some CPUs (and especially SIMD instructions like SSE) require data to be aligned to 8, 16, or even 32 bytes.
- **Correctness**: On strict architectures, unaligned access can lead to faults or crashes.

Assembly offers alignment directives (like `.align` or `align`) to force memory to align properly.

## 🧱 Simulating Structs and Arrays

Assembly doesn’t support structs or arrays directly, but you can simulate them using labels and offsets.

```asm
person:
    db name, 20      ; 20 bytes for the name
    dw age           ; 2 bytes for the age
```

You can use fixed offsets to access fields like in a C struct.

## 🧮 Floating-Point Numbers

Floating-point operations in x86 are supported by:

- **x87 FPU**: The legacy floating-point unit
- **SSE/AVX**: Modern SIMD instruction sets for faster operations on FLOAT and DOUBLE

Using `SSE` and `AVX` improves performance significantly for parallel math operations.

## 🧠 Registers and Data Sizes

| Register | Size   |
|----------|--------|
| AL, AH   | 8 bit  |
| AX       | 16 bit |
| EAX      | 32 bit |
| RAX      | 64 bit |

Each register corresponds to a data type size, and many instructions require matching sizes.

## 🌀 Understanding Little Endian

x86 architecture is **Little Endian**, meaning the least significant byte (LSB) is stored first in memory.

Example: The DWORD value `0x12345678` is stored as:

```
Address:     0x00   0x01   0x02   0x03
Content:     0x78   0x56   0x34   0x12
```

This byte order matters when reading/writing memory manually, debugging, or implementing network protocols (which often use Big Endian).

## 🔧 Code Examples

```asm
mov al, 0xFF        ; BYTE
mov ax, 0x1234      ; WORD
mov eax, 0xDEADBEEF ; DWORD
mov rax, 0xCAFEBABECAFEBABE ; QWORD
```

Each of these instructions shows how to load a value into a specific register corresponding to its type.

## ✅ Conclusion

Understanding x86 Assembly data types is fundamental for any low-level programmer, reverse engineer, or performance-minded developer.  
By mastering how data is represented, aligned, and accessed in memory — especially concepts like endianness — you can write faster, safer, and more effective assembly code.
