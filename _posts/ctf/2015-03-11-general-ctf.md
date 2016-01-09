---
layout: note
title: General CTF
date: 2015-03-11 00:00:00
categories: CTF
---

# General CTF Stuff

[Good link for CTF resources](https://github.com/ctfs/resources)

## Useful tips

- Doesn't output the trailing newline

```
echo -n
```

- Search for 'key' 'flag' 'unlock'

## Useful utilities
cmp (unix command)

# Reverse Engineering

### Commands

`$ strings bo | grep ‘flag’`

Search through the text for flag

### Tools

Building

- `nasm` : assembly compiler


### Identification

- `file`


### Disassemblers

- Static
- Hopper
- 64_dbg
- Visual DuxDebugger
- PE Explorer’s disassembler
- Hiew
- radare2
- [https://github.com/wibiti/uncompyle2](uncompyle2)

# Forensics

### PDF

- [http://sandsprite.com/blogs/index.php?uid=7&pid=57](PDF Stream Dumper)
- [http://qpdf.sourceforge.net/](qpdf)
- [http://blog.didierstevens.com/programs/pdf-tools/](PDF Tools)

### Editing

- [http://www.sweetscape.com/010editor/](010 editor): Powerful hex editor

# Exploitation


# Crypto

### Ideas / Methods

- Find out the method of encryption
- Look for known weaknesses in the protocols
- Look for differences between implementation and theoretical

# Frameworks

- [https://github.com/Gallopsled/pwntools](pwntools)
