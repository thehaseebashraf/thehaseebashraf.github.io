---
title: "Taks 1"
date: 2021-04-22T00:36:14+05:00
image: ""
draft: false

---
### Tools used:
1. Visual Studio Code
2. Docker 
1. QEMU
4. Hugo





* Firstly, we use VS code to setup our required files. Our task is to print OK on the screen for which we use some packages using RUN command. We use NASM to compile the code and grub package to get the final file.

- The header.asm and main.asm files are contained in the SRC folder. We used two label for start and end of header. Here we add the magic number and length. We named it as section which helped us in the final stage of linking. We added two dw’s and dd at the end set to zero to show that we dont have any more data.

+  We created the stack in our Main.asm file for storing all the local function calls data. It also helped in running C code that handled all stack manipulation files. In order to shift our kernel operating system to 64 bit mode we checked for multiboot, CPU ID (to check whether the cpu supports long mode or not) and then long mode. Page tables were also built inside main.asm file
* hlt is used to freeze the cpu.


- Linker.ld  is used to describe how to link our operatring system together. Entry is used as entrypoint named as start. We then defined each section individually. Boot folder is used to keep the multiboot header we defined in header.asm


+ grub.cfg is used to get the iso file because in most cases if you want to put your os in USB you need iso file.

* In make file we created 2 variables that held all the source and object files inside src/impl/x86_64/boot. After this we defined the commands that will be used to build our object files into source files. And another to hold our compiled file. Nasm was used to compile the assembly program. After writing the code for compiling the file we built a custom command build-x86_64 which ran when only our object file was changed. We created a directory for storing our iso file. At last, we used grub rescue command to generate our iso file.

* Main64.asm file is used to convert our operating system into 64-bit mode.

* Main.c file will contain the basics of the screen i.e foreground color, background color and the text to be displayed on the screen.

* Print.h file will be a header file that will create some methods and some an enum of colours.

* Print.c file contained a custom print function and some other methods associated with it.

* In the end, we ran qemu for simulating our operating system through the command qemu-system-x86_64 -cdrom dist/x86_64/kernel.iso