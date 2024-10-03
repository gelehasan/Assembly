
List of things to understand

When you run your text editor code, its being compiled which means your code being translated to a machine instruction, each operation is comprised of sequence of bites called an operaiton code (op code). trying to read op code is almost impossible 

4 main components in C programs

- Heap (designed for manually memory allocation) when ever these functions are called malloc, calloc, global , variables static are declared

Stack has 2 elements push and pop, each stack is assigned a stack address. Elements on the higher stack has a lower address than the bottom ones. Whenever a function is called its set up with a stack frame. all the local functions will be stored in that function stack frame.

EBP register also known as the base pointer contains the address of the base of the current stack frame

Esp register contains which is also referred to as the stack pointer contains the address of the top element of the current stack frame

The space between esp and ebp make up whatever the function is being called and the stack address outside are considered junk by the compiler.

Stack in practice when called

![image](https://github.com/user-attachments/assets/3415f91b-6383-4348-9888-cc04e9470705)



# Intro to assembly

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

1. Value argument of the stack 10 is pushed into the stack
2. return address is pushed to the stack which is a 4 byte and executed whenever the function is out of scope
3. Base pointer is pushed into the stack
4. Stack pointer is given the value of the base pointer
5. Finally the stack is incremented to make a room for the local variables

Good to know:

depending the compiler number of stack pointer is decremented by might be different.

All the space in memory between the pointer and the base is the function stack frame.

This sequence of instruction is called function prologue and its performed whenever a function is called


about the func function:

our first value is initialized to 0 so it will be pushed to the address of 0x4 (intiger is 4 bytes)

Now to get the location of our first value a its: **ebp - 0x4**

Now its time for the second variable, in this case our argument X **is 8 bytes below our base pointer and its not part of our stack frame,** since we declared a variable which x has to be assigned to, the variable argument needs to be moved inside the stack frame. but the problem is

- Value of the stack cannot be moved to another location on the stack without a general register
- The value of  our function argument must first be copied to one of our general purpose registers
- Then the value is moved 4 bytes below our first variable and 8 bytes below the base pointer

So now our varibale B has a memory address of ebp- 0x8

- Registers small areas in the processors, they are used to store memory addresses, values or anything that can be represented with 8 bytes or less. in x84 version there is 6 general purpose registers such as: eax, ebx, ECX, edx, ESI and EDI. reserved rgs: EBP, ESP and EIP
- Instructions

Assembly format

Every assembly instruction has 2 parts, **operation and argument**

operation can take 1 or 2 argument

move instruction takes 2 argument and copies the value referred to by the second argument  into the location referred by the first argument

Take the example you want to move a local varible to eax register

So if the command is eax,ebp-0x8  **it will not move 0x8, because ebp0-08x is adress of the stack where our variable  is located, so this instruction instead will copy our address of our variable into  the register**

In order to copy the actual value and whats **ebp-0x8**  is pointed to we need to use square

move eax,[ebp-0x8] // derefence  now we referecning the value


add takes 2 arguments, it stores the result into the first argument

eax=10

add eax,0x5

eax updated:
eax=15


Sub instruction works the same

Push/ pop

push places its operand onto the top of stack, it first decrements the stack pointer then place its operand into the location that it points to

push arg

pop reg

pop instruction takes a register as an argument, it will move the top element of the stack into the register specified by the its argument, then increments the stack pointer thus popping the top element off the stack
![image](https://github.com/user-attachments/assets/585673d9-8515-441f-a4a8-680f2672f446)

Lea instruction ( load, effective address

it places the address specified by the second operand into the register specified by its first operand

Which is used to obtaining a pointer into a memory region

Every instruction has an instruction address these are the memory where each instruction is stored

Eip register always contains the instruction thats currently being executed

So the computer will execute whatever the eip is pointing to

![image](https://github.com/user-attachments/assets/6442baac-46fd-4dd9-895e-28379b6135de)

So the computer will execute whatever the eip is pointing to

The compare instruction is equivalent to the sub instruction, except for storing results into the first argument it will contain flags in the processor that has 0, <0, >0

Compared instruction are always followed by a jump instruction

Every jmp instruction contains an instruction argument, it will check the state of the flag and set the instruction pointer into its argument.

There are many types of jump instruction

Jump equal to, jump not equal to, jump greater than

je, jne, jg
![image](https://github.com/user-attachments/assets/5e5261de-6ab9-4dc7-bc72-77ccde5acc47)
![image](https://github.com/user-attachments/assets/c1868300-53b7-49ae-8fa8-979a89599601)
if instruction earlier, compare 1,3 is followed by jump if less then. the jump would be taken
![image](https://github.com/user-attachments/assets/3cac0197-68ab-4520-8fd8-b06e1f4199d4)
But instead if we had jump if greater than, then the jump would not have taken and would just continue with the next instruciton

Call calls a function, it can be self made function or system functions such as printf etc.

Call takes one argument its equivalent to push eip, jump function. which means it will push the return address of the function being called into the stack then move eip to the first instruction of the function

The leave function is called at the end of every function, it destroys the current stack frame by setting the stack pointer to base pointer and popping the base pointer to off the top of the stack

The return instruction always follows a leave instruction

The return instruction will pop the return address off the top of the stack then set the instruction pointer to that address

## Summerzing

Think of assembly registers like a bucket used to store information

- **x86** = 32-bit —> can access up to 4GB of RAM
- **x64** = 64-bit —> handles much larger data

Words is just 2 bytes of data

Double word is 4 bytes of data

qWord is eight bytes of data

Stack follows last in first out data structure basically pop and push. here is where local variables and the code is stored

Flags(is a bits of register) used to set or not. can mean something and based on their value execute different acitons
00:     Carry Flag
01:     always 1
02:     Parity Flag
03:     always 0
04:     Adjust Flag
05:     always 0
06:     Zero Flag
07:     Sign Flag
08:     Trap Flag
09:     Interruption Flag     
10:     Direction Flag
11:     Overflow Flag
12:     I/O Privilege Field lower bit
13:     I/O Privilege Field higher bit
14:     Nested Task Flag
15:     Resume Flag

Instructions

**Move instruction:** moves one data from one register to another

// this will move rdx register to the rax register
move rax,rdx

// pointer is a value that points to a particular memory address
// extracting whatever the value rdx is pointing to and storing it in rax register
move, rax, [rdx]

// will move rdx register, to the memory pointed by the rax register, actual value of the rax
// register does not change
move [rax], rdx
