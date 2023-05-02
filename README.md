# Shellcode Creation

The Week's Assignment and Lab focuses on experimenting with creating Linux shellcode in x86_64 assembly.

---

# ANSWERS TO THE QUESTIONS

## 1) A code block containing my assembly instructions for your shellcode

```
.section .data
.section .text
    .global _start

_start:
    xor %rax, %rax
    xor %rdi, %rdi
    mov $0x0b, %al

    push %rdi
    mov $0x68732f6e69622f2f, %rdi
    push %rdi
    mov %rsp, %rdi

    xor %rsi, %rsi
    xor %rdx, %rdx
    syscall
```

## 2) A step-by-step explanation of your assembly code and how it sets up the system call

In the above code SECTION .data is where you store the data or define static variables. But since we are in need of op-codes, we cannot define a variable because variables do not have op-codes. So, we need to push the data directly to register. The SECTION .text is the section where we put our code at. We also have other sections such as SECTION .bss which is used for variables that are not initialized and are used to store user’s input data and etc.
`section .text` declares the section of the code as text and `global _start` declares the label "_start" as global, so that it can be accessed from 
outside the file. In addition `_start` is the entry point for the code. Also the instruction `xor rax, rax`,`xor rdi, rdi` ,`xor rsi, rsi` and `xor rdx, rdx` clears the rax, rdi, rsi and rdx registers respectively. Furthermore, the instruction `mov rdi, 0x0068732f6e69622f` stores the string "/bin/sh" in rdi in hexadecimal format. Moreover `mov al, 0x3b` sets rax to the value of the "execve syscall number". Lastly, `syscall` executes the  execve syscall to execute the shell.



## 3) Report on how many bytes total are in your assembly, and include the whole thing in ascii

My shellcode is 38 bytes long. Here they are: 48 31 c0 48 31 ff b0 3b 57 48 bf 2f 2f 62 69 6e 2f 73 68 57 48 89 e7 48 31 f6 48 31 d2 0f 05 
**ASCII:** 

## 4) Explanation of what I did to ensure there were no NULL bytes in my code
