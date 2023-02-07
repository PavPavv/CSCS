# 5. MEMORY ORGANIZATION AND ACCESS

80x86 family uses the von Neumann architecture (VNA) . A typical VNA has three major components:

- the central processing unit (CPU)
- memory
- input/output (I/O)

## The Data Bus

The CPU uses the data bus to move data between itself and memory.

CPUs use the data bus to shuttle data between the various components in a computer system. The size of this bus varies widely among CPUs. Indeed, bus size (or width ) is one of the main attributes that defines the “size” of the processor.
Most modern, general-purpose CPUs (such as those in PCs) employ a 32-bit-wide or, more commonly, 64-bit-wide data bus. Some processors use 8-bit or 16-bit data buses, and there may well be some CPUs with 128-bit data buses by the time you read this.

Older Intel 80x86 CPUs all have 64-bit buses but only 32-bit general-purpose integer registers, so they’re classified as 32- bit processors. The AMD (and newer Intel) x86-64 processors support 64-bit integer registers and a 64-bit bus, so they’re 64-bit processors.

With a single address bus line, a processor can access exactly two unique addresses: 0 and 1. With n address lines, the processor can access 2 n unique addresses (because there are 2 n unique values in an n -bit binary number). The number of bits on the address bus determines the maximum number of addressable memory and I/O locations.

| Processor                | Address bus size | Maximum addressable memory |
| ------------------------ | ---------------- | -------------------------- |
| 8088, 8086, 80186, 80188 | 20               | 1,048,576 (1MB)            |
| 80286, 80386sx           | 24               | 16,777,216 (16MB)          |
| 80386dx                  | 32               | 4,294,976,296 (4GB)        |
| 80486, Pentium           | 32               | 4,294,976,296 (4GB)        |
| Pentium Pro, II, III, IV | 36               | 68,719,476,736 (64GB)      |
| Core, i3, i5, i7, i9     | ≥40              | ≥1,099,511,627,776(≥1TB)   |

On modern processors, CPU manufacturers are building memory controllers directly onto the CPU. Instead of having a traditional address and data bus to which you connect arbitrary memory devices, newer CPUs contain specialized buses intended to talk to very specific dynamic random-access memory (DRAM) modules. A typical CPU’s memory controller connects to only a certain number of DRAM modules; thus, the maximum DRAM you can easily connect to a CPU is a function of the memory control built into the CPU rather than the size of the external address bus.

## The Control Bus

The system uses two lines on the control bus, read and write , to determine the data ﬂow direction (CPU to memory, or memory to CPU). So, when the CPU wants to write data to memory, it asserts (places a signal on) the write control line. When the CPU wants to read data from memory, it asserts the read control line.

The system clock lines, interrupt lines, status lines, and byte enable lines—are common to all processors.

## Physical Organization of Memory

The basic memory unit is a byte.
With address buses containing 20, 24, 32, 36, or 40 address lines, the 80x86 processors can address 1MB, 16MB, 4GB, 64GB, or 1TB of memory, respectively.

Think of memory as an array of bytes. The address of the first byte is 0 and the address of the last byte is 2 n – 1.

The address for a word or a double word is the address of its LO byte.
