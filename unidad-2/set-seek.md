# Unidad 2

## 🔎 Fase: Set + Seek

### ACTIVIDAD 1

Evidencias:

``` asm
@SCREEN
M=1
```

<img width="1864" height="486" alt="image" src="https://github.com/user-attachments/assets/5282f29a-cdc7-421a-902e-8ed9b0971d65" />
<img width="958" height="410" alt="image" src="https://github.com/user-attachments/assets/80d3e221-899b-47cf-885d-38e5afb842a9" />


### ACTIVIDAD 2

<img width="916" height="336" alt="image" src="https://github.com/user-attachments/assets/95cb708b-1a47-4fd9-8430-b871cf3e5301" />
<img width="1859" height="568" alt="image" src="https://github.com/user-attachments/assets/61432bc2-68c6-4f59-ac20-ffe6a20d8bfc" />

### ACTIVIDAD 3 

<img width="1865" height="506" alt="image" src="https://github.com/user-attachments/assets/65789a20-e1fc-4dc3-a5fc-f50841ba2266" />
<img width="1048" height="510" alt="image" src="https://github.com/user-attachments/assets/10e3c8e7-8a3a-4076-a814-9edc2044c669" />

``` asm
@SCREEN
M=-1
@CONTADOR
M=0

(LEER)

@KBD
D=M
@100
D=D-A
@DERECHA
D;JEQ


@KBD
D=M
@105
D=D-A
@IZQUIERDA
D;JEQ

@LEER
0;JMP

(DERECHA)
@CONTADOR
D=M
@SCREEN
A=D+A
M=0


@CONTADOR
M=M+1
D=M
@SCREEN
A=D+A

M=-1
@LEER
0;JMP

(IZQUIERDA)
@CONTADOR 
D=M
@SCREEN
A=D+A
M=0

@CONTADOR
M=M-1
D=M
@SCREEN
A=D+A

M=-1

@LEER
0;JMP
```

### Actividad 4

``` c++
int sum=0;
for(int i = 1; i <=100; i++){
   sum+= i;
}
```
ahora lo pasamos a asm

``` asm
// Adds1+...+100.
 @i // i refers to some memory location.
 M=1 // i=1
 @sum // sum refers to some memory location.
 M=0 // sum=0
 (LOOP)
 @i
 D=M // D=i
 @100
 D=D-A // D=i-100
 @END
 D;JGT // If(i-100)>0 gotoEND
 @i
 D=M // D=i
 @sum
 M=D+M // sum=sum+i
 @i
 M=M+1 // i=i+1
 @LOOP
 0;JMP // GotoLOOP
 (END)
 @END
 0;JMP // Infinite loop
```

Un puntero es una variable en la que se guarda un valor entero

int* ptr; declaro un puntero : ptr

ptr es una variable que guarda direcciones de otras variables


int i = 5;
int * ptr = &5; definicion y declaracion de variable

int j = ptr;

### Actividad 5

& es pa llamar direccion

seria

``` c++
int j = *ptr //ptr es el puntero
para escribir con el puntero es
```
``` c++
*ptr = 25 // se escribe en el puntero el valor que se quiere ingresar
```

### Actividad 5

``` c++
int a = 10;
int* p;
p = &a;
*p = 20;
```

ahora en asm

``` asm
@10
D=A
@16
M=D
@16
D=A
@17
M=D
@17
A=M
@20
D=A
M=D
```

siguiente codigo de c++

``` c++
int a = 10;
int b = 5;
int *p;
p = &a;
b = *p;
```

``` asm
@10
D=A
@16
M=D
@5
D=A
@17
M=D
@16
D=A
@18
M=D
@18
A=M
D=M
@17
M=D
``` 
el codigo primero pone el numero 10 en la variable a, y el numero 5 en la variable b. Luego crea un puntero p, y le guarda la direccion donde esta a. Al final, usa ese puntero para leer el valor de a, y se lo pone a b. Entonces, b que antes tenia 5, ahora queda con el mismo valor de a, o sea 10.












