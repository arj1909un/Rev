# SOLVE
we have to disassemble main and then check the eax register 
eax register stores the return value of the funcn in this chall the funcn is main.
to run gdb we have to run certain cmnds
## SETUP
```bash
docker run -it --platform linux/amd64 \
--cap-add=SYS_PTRACE \
--security-opt seccomp=unconfined \
-v $(pwd):/workspace \
gdb-env
```
```bash
cd /workspace
```
`gdb ./filename`
now we  have setup gdb and try to inspect main ,this is the code we run
```bash
(gdb) disassemble main
Dump of assembler code for function main:
   0x0000000000001129 <+0>:	endbr64
   0x000000000000112d <+4>:	push   %rbp
   0x000000000000112e <+5>:	mov    %rsp,%rbp
   0x0000000000001131 <+8>:	mov    %edi,-0x4(%rbp)
   0x0000000000001134 <+11>:	mov    %rsi,-0x10(%rbp)
   0x0000000000001138 <+15>:	mov    $0x86342,%eax
   0x000000000000113d <+20>:	pop    %rbp
   0x000000000000113e <+21>:	ret
End of assembler dump.
```
now we can see the value stored in the eax register
`0x86342` 
convert this hex to decimal and u will get the reqd digits for the flag
