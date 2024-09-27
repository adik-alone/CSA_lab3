<h1>CSA_Lab3</h1>
<h2>Цалов Василий P3207</h2>
<h2>Упрощёный вариант</h2>

``
asm | risc | harv | hw | instr | binary -> struct | trap -> stream | port | pstr | prob1 | cache
``

<h1>Язык программирования</h1>

```asm
<program> ::= { line }

<line> ::= <op_wo_arg> 
        | <op_one_arg> " " <term>
        | <op_arg> " " <term> 
        | <op_mem> " " <term> " " <term>
        | <op_data> " " <term> " " <term> " " <term>
        | <op_jump> " "<label_name> 
        | "section ." <term>
        | <label>
        | <label> <term>
        | "\n"

<op_without_arg> ::= "hlt"
                    | "write"
                    | "read"

<op_one_arg> ::= "inc"
                | "dec"
                   
<op_mem> ::= "load"
            | "store"
            
            
<op_data> ::= "add"
            | "sub" 
            | "mul" 
            | "div"
            | "mod"
            | "cmp"
       
           
<op_jump> ::= "jmp" 
            | "je"
 

<label> ::= <label_name> ":" {" "}


<letter> ::= [a-z] | [A-Z] 
<number> ::= ["-"] {0-9}- {<number>} 
<string> ::= {<letter> | <number>}-
<name> ::= <letter> {<string>}

<term> ::= <number> | <letter> | '"' <string> '"' | <reg_name> | <lable_name>

<label_name> ::= <name>
<reg_name> ::= "ra"
            | "rc"
            | "rd"
            | "rp"
            | "r5"
            | "r6"
            | "r7"
            | "r8"
```

```asm

load <lable_name> -> <reg_name>

```

15 команд\
Op_code\
hlt - 0 ----- 00000\
load - 1 ---- 00001\
store - 2 --- 00010\
mov - 3 ----- 00011\
[//]: # (setport - 3-- 00011\)

inc - 4 ----- 00100\
dec - 5 ----- 00101\
read - 6 ---- 00110\
write - 7 --- 00111\
add - 8 ----- 01000\
sub - 9 ----- 01001\
mul - 10 ---- 01010\
div - 11 ---- 01011\
mod - 12 ---- 01100\
jmp - 13 ---- 01101\
je - 14 ----- 01110\
cmp - 16 ---- 01111\


<h1>Программы</h1>

<h2>Cat</h2>

```asm
section .data

section .text
    _start:
        loop:
            load 0 rp
            read
            cmp '\n' rd
            je exit
            load 1 rp
            write rd
            jmp loop
        exit:
            hlt
```

<h2>Арифметика</h2>

```asm
section .data
a: 1
b: 2

section .text

    _start:
        load a r1
        load b r2
        add r1 r2 r3
        stroe r3 a
        hlt
```

<h2>Строки</h2>

```asm
section .data
message_size: 13
message: "Hello, world!"

section .text

_start:
    load message_size rc
    load message rd
    load 1 rp
    
    loop:
        write
        dec rc
        load 0 ra
        cmp ra rc
        je exit
        inc rd
        jmp loop
    exit:
        hlt
```

<h1>Организация памяти</h1>

```asm
Registers
+------------------------------+
| ra - accumulator             |
| rc - cycle                   |
| rd - data                    |
| rp - port                    |
| r4                           |
| ...                          |
| r9                           |
+------------------------------+

Instruction memory
+------------------------------+
| 00   : program start         |
|     ...                      |
| n    : hlt                   |
+------------------------------+

Data memory
+------------------------------+
| 00   : start_data            |
|     ...                      |
| n    : end_data              |
+------------------------------+
```
1. Литералы - 
2. Константы - 
3. Переменные - 
4. Инструкции - 
5. Процедуры - 
6. Прерывания во время компиляции