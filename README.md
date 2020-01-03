# MemorySegmentationExemplarCSharp

This program is my attempt to rewrite an exemplar program written in C found on pages 75-76 of 'Hacking: The Art of Exploitation' by Jon Erickson. The idea behind the program is to demonstrate the different segments
of memory that the program's code and data are allocated to. According to Erickson there are 5 main segments of memory: text (code) > data > bss > heap > stack (from lowest memory address to highest). 
The text segment contains the executable machine language instructions that the program is compiled into. Data contains initialised global and static variables, bss contains uninitialised global and static 
variables. Heap is dynamic memory that the programmer can allocate or free at will, and stack is used to store local variables and context during function calls. All of these are writable except for text.

Translating this program into C# was quite educational, and there were some aspects that I wasn't able to replicate. For example, static_var and static_initialised_var are not really static in this program,
because C# does not support local static variables. Moreover, I have made both class-level variables static so that they can be called by Main(). However, by far the biggest difference is how C# operates
with regard to memory management. Unlike C and C++, C# automatically manages memory for you. As far as I can make out, C# stores program data in the heap and the stack. The heap seems to be used for non-local
variables (global_var and global_initialised_var), whereas local variables and function contexts are stored on the stack in stack frames. I presume that there is still a 'text' segment that the program
instructions are allocated to, but I don't know. I have no about data and bss, C# doesn't seem to allow code to compile with uninitialised variables. The order of segmentation also seems
different. As far as I can make out the stack addresses that local variables are stored in are lower than the heap addresses that globals go into. By far the highest address that any any of these variables
are allocated is the address that heap_var gets given. Heap_var is the variable that I manually allocate memory from the heap. I assume the address is significantly higher because it is placed after the end
of the CLR-managed heap and at the beginning of the 'unmanaged' heap.
