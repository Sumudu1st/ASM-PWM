# ASM-PWM
ALP code for P0.0 high 10 ms and low 10 ms by using software delays.

#### Code Explanation

Defining the start memory location
``` asm
ORG 000H
```
Clearing the port 0
``` asm
MOV P0,#00000000B
```
This is a common techniq used to make sure that pins has not assigned any values or it is on low state.

Running the main function
``` asm
MAIN: ACALL DELAY
      SETB P0.0
      ACALL DELAY
      CLR P0.0
      SJMP MAIN
 ```
`MAIN` is a lable. you can add whatever you want there.  
`ACALL DELAY` calling the code in the lable `DELAY`.  
`SETB P0.0` setting the bit/pin 0 in port 0 high.   
Keeps it high with DELAY  
`CLR P0.0` clearing the bit/pin by making the value 0  
`SJMP MAIN` jump to the lable `MAIN`.  

Software delay
``` asm
DELAY:MOV R2,#10
      L1:DJNZ R2,L1
      RET 
```
In here I assumed the time to run `DJNZ` line/instruction is 1ms.

`MOV R2,#10` assigning value of decimal 10 to `R2`.  
`L1:DJNZ R2,L1` Decrement the value in `R2` by 1 and jump to lable `L1` if the remaining value in `R2` is zero. It keeps doing until the value becomes zero and the go to next instruction.

`RET` go to the previous location.

End of the program.

``` asm
END
```

This simple code made on a request for 8051 micro controller and tested on a simulator. If there are any faults on the explanation please correct me. 
