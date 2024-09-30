
List of things to understand

When you run your text editor code, its being compiled which means your code being translated to a machine instruction, each operation is comprised of sequence of bites called an operaiton code (op code). trying to read op code is almost impossible 

4 main components in C programs

- Heap (designed for manually memory allocation) when ever these functions are called malloc, calloc, global , variables static are declared

Stack has 2 elements push and pop, each stack is assigned a stack address. Elements on the higher stack has a lower address than the bottom ones. Whenever a function is called its set up with a stack frame. all the local functions will be stored in that function stack frame.

EBP register also known as the base pointer contains the address of the base of the current stack frame

Esp register contains which is also referred to as the stack pointer contains the address of the top element of the current stack frame

The space between esp and ebp make up whatever the function is being called and the stack address outside are considered junk by the compiler.

Stack in practice when called

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9d211471-2b1d-4707-9027-75d9ae2583a0/4ceca409-d893-4e5c-ac88-4ea9dd83b3e3/image.png)
