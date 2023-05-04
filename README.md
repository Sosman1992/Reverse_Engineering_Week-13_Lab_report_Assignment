# Shellcode Creation

The Week's Assignment and Lab focuses on experimenting with creating Linux shellcode in x86_64 assembly.

---

# ANSWERS TO THE QUESTIONS

## 1) A code block containing my assembly instructions for your shellcode

```
.section .text
.global _start

_start:
    # push a 64-bit zero onto the stack
    pushq $0
    # save the current stack pointer in rdx and push it onto the stack
    movq %rsp, %rdx
    pushq %rdx
    # save the current stack pointer in rsi and rdx
    movq %rsp, %rsi
    movq %rsp, %rdx
    # load the string "/bin/sh" into rax and push it onto the stack
    movabsq $0x0068732F6E69622F, %rax
    pushq %rax
    # save the address of the string in rdi
    movq %rsp, %rdi
    # set rax to 59 (the system call number for execve) and rbx to an arbitrary value
    movq $59, %rax
    xorq %rbx, %rbx
    # make the system call
    syscall

```

## 2) A step-by-step explanation of your assembly code and how it sets up the system call

In the above code SECTION .data is where you store the data or define static variables. But since we are in need of op-codes, we cannot define a variable because variables do not have op-codes. So, we need to push the data directly to register. The SECTION .text is the section where we put our code at. We also have other sections such as SECTION .bss which is used for variables that are not initialized and are used to store user’s input data and etc.
`section .text` declares the section of the code as text and `global _start` declares the label "_start" as global, so that it can be accessed from 
outside the file. In addition `_start` is the entry point for the code. The instruction pushq $0 pushes a 64-bit zero onto the stack. This is needed as the first argument to the execve system call later. Also, the instruction movq %rsp, %rdx saves the current stack pointer in the %rdx register. The %rsp register contains the address of the top of the stack, so this instruction effectively saves the address of the stack. Moreover, the instruction pushq %rdx pushes the address of the stack onto the stack itself. This is needed as the second argument to the execve system call later. Furthermore, the instruction movabsq $0x0068732F6E69622F, %rax loads the string "/bin/sh" into the %rax register. In addition, the instruction pushq %rax pushes the address of the string "/bin/sh" onto the stack. This is needed as the first argument to the execve system call later. The instruction movq %rsp, %rdi then saves the address of the string "/bin/sh" in the %rdi register. This register will be used as the first argument to the execve system call later. Lastly, the instruction movq $59, %rax sets the %rax register to the value 59, which is the system call number for execve.


## 3) Report on how many bytes total are in your assembly, and include the whole thing in ascii

My shellcode is 38 bytes long. Here they are:
f348484874ff48c3fff20ff368f290f368f290f368f290f368f290f368f290f368f290off3f20ff3f20ff3f20ff3f20ff3f20ff3f20ff331495e48485054453148fff46600f3c3660090b84874b84874bfff66c366000fbe48484848484874b84874bfffc366000ff380755548e8c65dc390c366000ff3ebf355484889486400483148484848e848480075484848484848b8e8b8e9484848babe48e8894848e8484848b8e883758b48894848b8e8b8eb4848e848b8ff48b848640074e8c9c3f34848c3

**ASCII:** 

## 4) Explanation of what I did to ensure there were no NULL bytes in my code
