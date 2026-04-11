# SOLVE
Same task as before but this time we try to run it on the command line with input "Hello!"?.

Why command-line arguments?
The program is written to receive input as an argument rather than typing it interactively.

so same docker as before using this cmnd
```bash
docker run --rm --platform linux/amd64 -v $(pwd):/work -w /work ubuntu ./run "Hello!"
```
we get this as an output on our screen
`dquote> `
after searching abt what it means i found out that it means our string hasn't been enclosed yet.
So in single quotes, ! is just the character ! — nothing special. In double quotes, zsh sees ! and tries to do history expansion, which breaks things.

## FLAG
`picoCTF{F1r57_4rgum3n7_be0714da}`
