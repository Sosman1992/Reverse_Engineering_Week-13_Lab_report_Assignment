# Shellcode Creation
https://wajid-nawazish.medium.com/developing-custom-shellcode-in-x64-57172a885d77,https://wajid-nawazish.medium.com/developing-custom-shellcode-in-x64-57172a885d77,https://masterccc.github.io/memo/shellcode/
The Week's Assignment and Lab focuses on experimenting with creating Linux shellcode in x86_64 assembly.

---

# ANSWERS TO THE QUESTIONS

## 1) A code block containing my assembly instructions for your shellcode

'''
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


## 3) Report how many bytes total are in your assembly, and include the whole thing in ascii

A. The easiest way to get this information is probably with a quick python script 
B. Example: My shellcode is 35 bytes long. Here they are: -- 4A FE 56 08 ...


## 4) Explanation of what I did to ensure there were no NULL bytes in my code
