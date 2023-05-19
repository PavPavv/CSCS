# 5. MEMORY ORGANIZATION AND ACCESS

80x86 family uses the von Neumann architecture (VNA) . A typical VNA has three major components:

- the central processing unit (CPU)
- memory
- input/output (I/O)

## Physical Organization of Memory

The basic memory unit is a byte.
With address buses containing 20, 24, 32, 36, or 40 address lines, the 80x86 processors can address 1MB, 16MB, 4GB, 64GB, or 1TB of memory, respectively.

Think of memory as an array of bytes. The address of the first byte is 0 and the address of the last byte is 2 n – 1.

The address for a word or a double word is the address of its LO byte.

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

### 8-Bit Data Buses

A processor with an 8-bit bus (like the old 8088 CPU) can transfer 8 bits of data at a time.

### 16-Bit Data Buses

Some CPUs (such as the 8086, the 80286, and variants of the ARM processor family) have a 16-bit data bus. This allows these processors to access twice as much memory in the same amount of time as their 8-bit counterparts. These processors organize memory into two banks : an “even” bank and an “odd” bank

### 32-Bit Data Buses

The 80x86 processors with a 32-bit data bus, such as the Pentium and Core processors, use four banks of memory connected to the 32-bit data bus. A 32-bit CPU can access a double word in a single memory operation only if the address of that value is evenly divisible by 4. If not, the CPU may require two memory operations.

### 64-Bit Data Buses

The Pentium and later processors, like Intel i-Series, provide a 64-bit data bus and special cache memory that reduces the impact of nonaligned data access.

#### Small Accesses on Non-80x86 Processors

Most RISC processors, including those found in modern smartphones and tablets (typically ARM processors), do not allow you to access byte and word objects at all. Most RISC CPUs require that all data accesses be the same size as the data bus (or general-purpose integer register size, whichever is smaller). This is generally a double- word (32-bit) or quad-word (64-bit) access. If you want to access bytes or words on such a machine, you have to treat them as packed fields an use the shift and mask techniques to extract or insert byte and word data in a double word. Although it’s nearly impossible to avoid byte accesses in software that does any character and string processing, if you expect your software to run efficiently on various modern RISC CPUs, you should avoid word data types (and the performance penalty for accessing them) in favor of double words.

#### Big-Endian vs. Little-Endian Organization

The byte organization that Intel uses is whimsically known as the little-endian byte organization . The alternate form is known as big-endian byte organization .

```c
union
{
unsigned long bits32; /* This assumes that C uses 32 bits for
unsigned long */
unsigned char bytes[4];
} theValue;

theValue.bytes[0] = 0;
theValue.bytes[1] = 1;
theValue.bytes[2] = 0;
theValue.bytes[3] = 0;
isLittleEndian = theValue.bits32 == 256;
```

On a big-endian machine, this code sequence will store the value 1 into bit 16, producing a 32-bit value that is definitely not equal to 256, whereas on a little-endian machine this code will store the value 1 into bit 8, producing a 32-bit value equal to 256. Therefore, you can test the _isLittleEndian_ variable to determine whether the current machine is little- endian ( true ) or big-endian ( false ).

## The Control Bus

The system uses two lines on the control bus, read and write , to determine the data ﬂow direction (CPU to memory, or memory to CPU). So, when the CPU wants to write data to memory, it asserts (places a signal on) the write control line. When the CPU wants to read data from memory, it asserts the read control line.

The system clock lines, interrupt lines, status lines, and byte enable lines—are common to all processors.

## The System Clock

On von Neumann machines, most operations are serialized , which means that the computer executes commands in a prescribed order.

To execute statements in the proper order, the processor relies on the system clock , which serves as the timing standard within the system.
The system clock is an electrical signal on the control bus that alternates between 0 and 1 periodically.
All activity within the CPU is synchronized with the edges (rising or falling) of this clock signal.

> On most modern systems, the system clock frequency exceeds several billion cycles per second.

A typical Pentium IV chip, circa 2004, runs at speeds of three billion cycles per second or faster. Hertz (Hz) is the unit corresponding to one cycle per second, so the aforementioned Pentium chip runs at between 3,000 and 4,000 million hertz, or 3,000 to 4,000 megahertz (MHz), or 3 to 4 gigahertz (GHz, or one billion cycles per second).

Clock periods are usually expressed in microseconds or nanoseconds. To ensure synchronization, most CPUs start an operation on either the falling edge (when the clock goes from 1 to 0) or the rising edge (when the clock goes from 0 to 1).

Because all CPU operations are synchronized with the clock, the CPU cannot perform tasks any faster than the clock runs.

Memory access is an operation that is synchronized with the system clock; that is, memory access occurs no more than once every clock cycle. The memory access time is the number of clock cycles between a memory request (read or write) and when the memory operation completes.

Modern CPUs are much faster than memory devices, so systems built around these CPUs often use a second clock, the bus clock , which is some fraction of the CPU speed. For example, typical processors in the 100 MHz to 4 GHz range can use 1600 MHz, 800 MHz, 500 MHz, 400
MHz, 133 MHz, 100 MHz, or 66 MHz bus clocks (a given CPU generally supports several different bus speeds, and the exact range it
supports depends upon that CPU).

Memory devices have various ratings, but the two major ones are capacity and speed.

> the memory speed must match the bus speed or the system will fail

### Wait states

A wait state is an extra clock cycle that gives a device additional time to respond to the CPU.

Almost every general-purpose CPU in existence provides a pin (whose signal appears on the control bus) that allows you to insert wait states. If necessary, the memory address decoding circuitry asserts this signal to give the memory sufficient access time.

#### Cache Memory

if you paid an outrageous sum of money for expensive zero-wait-state RAM, you’d be using only a tiny fraction of it at any given time.

Cache memory is a small amount of very fast memory that sits between the CPU and main memory. Unlike in normal memory, the bytes within a cache do not have fixed addresses.
Cache memory can dynamically reassign addresses, which allows the system to keep recently accessed values in the cache. Addresses that the CPU has never accessed, or hasn’t accessed in some time, remain in main (slow) memory.

To take advantage of temporal locality of reference, the CPU copies data into the cache whenever it accesses an address that’s not present in the cache. Because the system will likely access that address shortly, it can save wait states on future accesses by
having that data in the cache.
