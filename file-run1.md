# SOLVE
hint says use `chmod +x` , which means add execute permission to the file fro the user running the command.
another hint says use `./` cmnd Normally when you type a command like ls or python, your system searches for it in standard system folders. But if your file is just sitting in your current folder, the system won't find it automatically — so you use ./ to say:
"Hey, run this file right here, in the current folder".
now i should have got he flag but i am using mac so i faced an error.

```bash
/lib64/ld-linux-x86-64
```
this means the file is only executable in a linux envoirnment also called an ELF (Executable Linkable Format).
and we got to know this by checking the file type using this cmnd
```bash
file run
```
and the output i got is
```bash
run: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=a468f05064d2f1ffa0047ba7295de4995176da15, for GNU/Linux 3.2.0, not stripped
```
so installed docker and ran this command
```bash
docker run --rm --platform linux/amd64 -v $(pwd):/work -w /work ubuntu ./run
```
and then i got the flag.

### IMP 
In docker i didn need to do chmod +x run cuz
Mac uses a virtual filesystem layer (via Docker Desktop) to bridge between macOS and Linux
Files mounted with -v from Mac often get execute permissions automatically because macOS and Docker Desktop are lenient about it behind the scenes
So the x bit gets set without you doing it manually.

<img width="754" height="298" alt="image" src="https://github.com/user-attachments/assets/e71351a6-2d2e-4879-8eba-0ad5773b354a" />


## Flag
`picoCTF{U51N6_Y0Ur_F1r57_F113_e5559d46}`
