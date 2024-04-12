# Linking Notes

### To prevent `stdlib` from linking
```console
gcc -nostdlib -o hello hello.c
```

### Compile a file but don't link
```console
gcc -Os -c hello.c
```

### Manually link two objects using linker
Here `ctr1.o` is present already and `hello.o` was created in the previous step. Both are linked to produce the ELF `hello`
```console
ld /usr/lib/crt1.o -o hello hello.o
```

### Compiling the source file with an assembly stub
```console
gcc -nostdlib stubstart.S -o hello hello.c
```


# Investigating objects and ELFs

Some important points from the [spec](./ELF_Spec.pdf):
* *Program header* refers to the "Program Header Table" (optional for the *Linker View*).
* *Section header* refers to the "Section Header Table" (optional for the *Executable View*)


### `objdump -d`
Only disassemble those sections which are expected to contain instructions.

### `objdump -D`
Disassemble the contents of all sections, not just those expected to contain instructions.

### `objdump -t`
This will print all the symbols and their respective sections:
* Column 1: the symbol's value/address.
* Column 2: a set of characters and spaces representing
the flag bits set for the symbol. There are 7 groupings, three of which
are represented in this symbol table. The first can be l, g,
<space>, or !, if the symbol is local, global, neither, or both,
respectively. The sixth can be d, D, or <space>, for debugging,
dynamic, or normal, respectively. The seventh can be F, f, O, or
<space>, for function, file, object, or normal symbol,
respectively. Descriptions of the 4 remaining grouping can be found in
that unusally comprehensive objdump manpage.
* Column 3: which section the symbol lives in. *ABS*, or absolute, means the symbol is not associated with a certain section.
* Column 4: the symbol's size/alignment.
* Column 5: the symbol's name.

### `objdump -s`
Print the contents of the sections with strings decoded

### `readelf -l`
Print the program headers of the ELF

### `readelf -S`
Print the section headers of the ELF


#### References:
* [Hello World from a libc-free world Part 1](https://blogs.oracle.com/linux/post/hello-from-a-libc-free-world-part-1) 

* [Hello World from a libc-free world Part 2](https://blogs.oracle.com/linux/post/hello-from-a-libc-free-world-part-2)