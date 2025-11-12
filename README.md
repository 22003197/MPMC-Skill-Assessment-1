# SKILL ASSESSMENT - 1
## Write an assembly language program in 8051 to find the largest number from a given set of N numbers stored in memory. Display the result in AL register.

## AIM :
To write and execute an 8051 assembly language program to find the largest number from a given set of N numbers stored in internal memory, and display the result in the Accumulator (A) register using Keil µVision.

## APARATUS REQUIRED :
Keil µVision5 IDE
Laptop

# ALGORITHM :
STEP 1 : Start the program and initialize the data pointer.

STEP 2 : Load N (the number of elements) from memory location 30H.

STEP 3 : Initialize registers:
         Set pointer register R0 to the first data element (31H).
         Move the first data element into register R3 as the initial maximum.

STEP 4 : Decrement N (since the first element is already considered).

STEP 5 : Compare each subsequent number with the current maximum:
         If the new number > current maximum → update the maximum.

STEP 6 : Repeat the comparison until all N elements are processed.

## PROGRAM :
```
; Program: Find the Largest Number from N numbers stored in internal RAM
; Author: Shruthi S
; Assembler: Keil µVision 8051 Assembler
; Result: Largest number displayed in A (Accumulator)

        ORG 0000H
START:  
        MOV     A, 30H       ; Load N (count)
        JZ      NO_DATA      ; If N = 0, skip
        MOV     R6, A        ; R6 = N
        MOV     R0, #31H     ; Pointer to first number
        MOV     A, @R0       ; Load first number
        MOV     R3, A        ; Store as current max
        INC     R0           ; Point to next number
        MOV     A, R6
        CJNE    A, #01H, CONTINUE ; If N=1, done

DONE:
        MOV     A, R3        ; Move max to A
        SJMP    $            ; Stop here

CONTINUE:
        MOV     A, R6
        DEC     A
        MOV     R6, A

LOOP1:
        MOV     A, @R0
        MOV     R4, A
        MOV     A, R4
        CLR     C
        SUBB    A, R3
        JC      SKIP_UPDATE
        MOV     A, R4
        MOV     R3, A

SKIP_UPDATE:
        INC     R0
        DJNZ    R6, LOOP1

        MOV     A, R3
        SJMP    $

NO_DATA:
        MOV     A, #00H
        SJMP    $

        END START
```

## OUTPUT : 

<img width="1920" height="1080" alt="Screenshot 2025-11-11 214511" src="https://github.com/user-attachments/assets/b24a265f-ec7c-46a2-a35d-732c56675aad" />

## RESULT :

The 8051 assembly program was successfully written, assembled, and simulated using Keil µVision5.
The largest number from the given set was correctly identified and stored in the Accumulator (A) register.
