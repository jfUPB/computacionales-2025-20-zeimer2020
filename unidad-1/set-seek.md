# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 3

``` asm
(LOOP)


@5
D=M
@10
D=D-A


@MENOR
D;JLT



(MAYOREQ)
@7
M=0
@LOOP
0;JMP


(MENOR)
@7
M=1
@LOOP
0;JMP
```
