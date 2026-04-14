# SOLVE

Dump of assembler code for function main:
```bash
   0x0000000000401106 <+0>:	endbr64
   0x000000000040110a <+4>:	push   %rbp
   0x000000000040110b <+5>:	mov    %rsp,%rbp
   0x000000000040110e <+8>:	mov    %edi,-0x14(%rbp)
   0x0000000000401111 <+11>:	mov    %rsi,-0x20(%rbp)
   0x0000000000401115 <+15>:	movl   $0x1e0da,-0x4(%rbp)
   0x000000000040111c <+22>:	movl   $0x25f,-0xc(%rbp)
   0x0000000000401123 <+29>:	movl   $0x0,-0x8(%rbp)
   0x000000000040112a <+36>:	jmp    0x401136 <main+48>
   0x000000000040112c <+38>:	mov    -0x8(%rbp),%eax
   0x000000000040112f <+41>:	add    %eax,-0x4(%rbp)
   0x0000000000401132 <+44>:	addl   $0x1,-0x8(%rbp)
   0x0000000000401136 <+48>:	mov    -0x8(%rbp),%eax
   0x0000000000401139 <+51>:	cmp    -0xc(%rbp),%eax
   0x000000000040113c <+54>:	jl     0x40112c <main+38>
   0x000000000040113e <+56>:	mov    -0x4(%rbp),%eax
   0x0000000000401141 <+59>:	pop    %rbp
   0x0000000000401142 <+60>:	ret
```
now we will brekdown this assembly code line by line

1. `0x000000000040110a <+4>:    push   %rbp`

this means that Save the current base pointer (rbp) onto the stack

rbp = base pointer register

-> It points to the current function’s stack frame

Now what happens is in functions the stack frame moves downward so as you increase the data in the function the stack pointer moves downward 

 the last reserved value (at the lowest address rsp) is called the "top" of the stack.

 2. `0x000000000040110b <+5>:	mov    %rsp,%rbp`

 Copies rsp into rbp so the function has a stable base to access its data.

Variables are accessed relative to rbp using fixed offsets, making it easier to reference both local variables and function arguments.

Now towards the important stuff

```bash
movl $0x1e0da,-0x4(%rbp)
movl $0x25f,-0xc(%rbp)
movl $0x0,-0x8(%rbp)
```

Define 3 variables:

var1 = 0x1e0da;    at rbp-4
var2 = 0x25f;      at rbp-12
i    = 0;          at rbp-8

3. `jmp 0x401136`

Skip loop body → go to condition first

```bash
mov -0x8(%rbp), %eax   → eax = i
cmp -0xc(%rbp), %eax   → compare i with var2
jl 0x40112c            → if i < var2 → loop
```
So, var1 += i; 
i++;

4. `mov -0x4(%rbp), %eax`

It is a return statement that returns var1

I we write the code in C it will be easier to get the output
```bash
int main() {
    int var1 = 123098;
    int var2 = 607;
    int i = 0;

    while (i < var2) {
        var1 += i;
        i++;
    }

    return var1;
}
```

Final value that EAX stores = 307019


