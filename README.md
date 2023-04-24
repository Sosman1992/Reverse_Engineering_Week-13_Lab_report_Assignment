# Shellcode Creation

The Week's Assignment and Lab focuses on experimenting with creating Linux shellcode in x86_64 assembly.

---

# ANSWERS TO THE QUESTIONS

## 1) A code block containing my assembly instructions for your shellcode

'''
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
'''

## 2) A step-by-step explanation of your assembly code and how it sets up the system call

In the above code SECTION .data is where you store the data or define static variables. But since we are in need of op-codes, we cannot define a variable because variables do not have op-codes. So, we need to push the data directly to register. The SECTION .text is the section where we put our code at. We also have other sections such as SECTION .bss which is used for variables that are not initialized and are used to store user’s input data and etc.

## 3) Report how many bytes total are in your assembly, and include the whole thing in ascii

A. The easiest way to get this information is probably with a quick python script 
B. Example: My shellcode is 35 bytes long. Here they are: -- 4A FE 56 08 ...


## 4) Explanation of what I did to ensure there were no NULL bytes in my code
