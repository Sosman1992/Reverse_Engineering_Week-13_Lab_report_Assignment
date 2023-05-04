# Shellcode Creation

The Week's Assignment and Lab focuses on experimenting with creating Linux shellcode in x86_64 assembly.

---

# ANSWERS TO THE QUESTIONS

## 1) A code block containing my assembly instructions for your shellcode

```
.section .text
.global _start

_start:
    # push 0 onto the stack
    pushq $0
    # save the current stack pointer in rdx
    movq %rsp, %rdx
    # push rdx onto the stack
    pushq %rdx
    # save the current stack pointer in rsi
    movq %rsp, %rsi
    # save the current stack pointer in rdx again
    movq %rsp, %rdx
    # load the string "/bin/sh" into rax
    movq $0x0068732F6E69622F, %rax
    # push the string onto the stack
    pushq %rax
    # save the address of the string in rdi
    movq %rsp, %rdi
    # set rax to 59 (the system call number for execve)
    movq $59, %rax
    # set rbx to 59 (arbitrary value)
    movq $59, %rbx
    # make the system call
    syscall
```

## 2) A step-by-step explanation of your assembly code and how it sets up the system call

In the above code SECTION .data is where you store the data or define static variables. But since we are in need of op-codes, we cannot define a variable because variables do not have op-codes. So, we need to push the data directly to register. The SECTION .text is the section where we put our code at. We also have other sections such as SECTION .bss which is used for variables that are not initialized and are used to store user’s input data and etc.
`section .text` declares the section of the code as text and `global _start` declares the label "_start" as global, so that it can be accessed from 
outside the file. In addition `_start` is the entry point for the code. Also the instruction `xor rax, rax`,`xor rdi, rdi` ,`xor rsi, rsi` and `xor rdx, rdx` clears the rax, rdi, rsi and rdx registers respectively. Furthermore, the instruction `mov rdi, 0x0068732f6e69622f` stores the string "/bin/sh" in rdi in hexadecimal format. Moreover `mov al, 0x3b` sets rax to the value of the "execve syscall number". Lastly, `syscall` executes the  execve syscall to execute the shell.



## 3) Report on how many bytes total are in your assembly, and include the whole thing in ascii

My shellcode is 41 bytes long. Here they are: 48 31 c0 48 31 ff b0 3b 57 48 bf 2f 2f 62 69 6e 2f 73 68 57 48 89 e7 48 31 f6 48 31 d2 0f 05 
**ASCII:** 

## 4) Explanation of what I did to ensure there were no NULL bytes in my code
