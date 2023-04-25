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

## 3) Report on how many bytes total are in your assembly, and include the whole thing in ascii

My shellcode is _ bytes long. Here they are: -- 48 31 d2 48 31 f6 48 b8 2f 62 69 6e 2f 73 68 00 50 48 89 e7 b8 3b 00 00 00 0f 05

## 4) Explanation of what I did to ensure there were no NULL bytes in my code
