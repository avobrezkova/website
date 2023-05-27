---
title: Methods of protection from attack type buffer overflow
subtitle: Methods of protection from attack type buffer overflow
# Summary for listings and search engines
summary: Methods of protection from attack type buffer overflow

# Link this post with a project
projects: []

# Date published
date: '2023-05-27T00:00:00Z'

# Date updated
lastmod: '2023-05-27T00:00:00Z'

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
  focal_point: ''
  placement: 2
  preview_only: false

authors:
  - admin
  - 

tags:
  - Academic
  - 

categories:
  - Demo
  - 
---

```python
import libr
print('hello')
```

## Buffer overflow

At its core, a buffer overflow is a surprisingly simple error that occurs as a result of normal practice. Computer programs often work with chunks of data that are read from a file, from the network, or even from the keyboard. Programs allocate blocks of memory of finite size - buffers - to hold this data as they work on it. A buffer overflow occurs when more data is written to or read from the buffer than it can hold.

## Techniques to protect against buffer overflow attacks: ASLR

Linux has some built-in mechanisms to prevent potentially malicious code execution in case of buffer overflow in a program. ASLR - Address Space Location Randomization - This randomizes the memory addresses used by a program each time it is run, this becomes an obstacle to an attacker because it prevents them from easily making a working exploit. For example, if the return address to which you want to redirect your program changes every time, it cannot be hard-coded into an exploit. This is a feature of the OS itself. To disable ASLR: This must be run again after a reboot, unless it is included in the startup script that is automatically run every time you boot up.

## Methods to protect against buffer overflow attack: DEP

DEP is data execution prevention. It marks some vulnerable parts in memory as non-executable. This is a feature of the compiler. Some directives can be used at compile time to disable such protections because they are enabled by default in gcc. The -fno-stack-protector parameter disables the stack part (canaries) and the -z execstack parameter makes both heap and stack executable.

## Methods to protect against buffer overflow attacks: tools during development

During development, there are tools that can analyze source code and running programs to try to detect dangerous constructs or overflow errors before those errors make their way into the finished software. For example, AddressSantizer (which is an open-source programming tool that detects memory corruption bugs such as buffer overflows or access to a dangling pointer), and older tools such as Valgrind (which is a software tool for debugging memory, memory leak detection, and profiling) offer such capabilities. However, these tools require the active participation of the developer.

##Methods to protect against buffer overflow attacks: some systems

Perhaps the most important is the protection known under different names W^X (“write exclusive-or execute”), DEP (“data execution prevention”), NX (“No Xecute”), XD (“eXecute Disable”), EVP (“Enhanced Virus Protection”, a rather unusual term sometimes used by AMD), XN (“eXecute Never”) and probably others. The principle here is simple. These systems tend to make memory either writable (buffer-worthy) or executable (library and program code-worthy), but not both. Thus, even if an attacker can overflow a buffer and control the return address, the processor will eventually refuse to execute the shellcode.

## Methods to protect against buffer overflow attacks: the non-executable stack

An unexecutable stack prevents executing code in the stack (or dynamic memory) memory region and writing executable code, which can in some cases prevent the exploitation of a buffer overflow. Thus, it is impossible to exploit a buffer overflow by injecting executable code into the stack if a non-executable stack is used.








